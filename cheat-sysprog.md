
# Systems Programming

## Memory

### Virtual Memory
- Page size: 4KB = 4096 bytes
- Logical Address = (Logical Page Number, Offset)
- Physical Address = (Physical Page Number, Offset)
- Page Table = Logical Page Number -> Physical Page Number
- On Demand Paging
- Major Page Fault -- Page does not exist yet, needs to be created from disk
- Pages are shared between processes
- Copy on write (On Demand Memory/Paging)
- Special pages - swap page, zero page, read data behavior, write data behavior, anonymous vs file backed pages

```text
cat /proc/meminfo
Mem

ls /sys/devices/system/ /proc/sys/vm/

numactl --hardware
free
top
dmesg

ls /proc/pid/status,*maps
ps

ulimit -a  # how much memory can a process use
```

### Shared memory Anonymous

Can be shared with a child process, that

```cpp
size_t buffer_size = 32MB;
int flags = MAP_ANONYMOUS | MAP_SHARED | MAP_POPULATE;
flags |= MAP_HUGETLB | (30<<MAP_HUGE_SHIFT);                // 1gb hugepage
void* buf = mmap(
  nullptr,
  buffer_size,
  PROT_WRITE|PROT_READ,
  flags,
  -1,
  0
);
assert(buf != MAP_FAILED);
madvise(buf, buffer_size, MADV_WILLNEED|MADV_UNMERGABLE|MADV_HUGEPAGE);
memset(buf, 0, buffer_size);
int err = mlock(buf, buffer_size);
assert(err >= 0);
...
err = munmap(buf, buffer_size);
assert(err >= 0);

```

### Shm Named File

Can be shared with anybody who has access to the named shared mem file. Use `shm_open()` to open a shared memory object

```cpp
const string name = "/dev/shm/blah.shm";
int fd = ::shm_open(name.c_str(), O_EXCL | O_CREAT | O_RDWR, S_IRWXU | S_IRWXG | S_IRWXO);
assert(fd >= 0);
ftruncate(fd, buffer_size);
void* buf = mmap(nullptr, buffer_size, PROT_READ | PROT_WRITE, MAP_SHARED | MAP_POPULAT | MAP_LOCKED, fd, 0);
assert(buf != MAP_FAILED);
...
munmap(buf, buffer_size);
shm_unlink(name.c_str());
```

### Shared memory segment IPC
```cpp
int buffer_size = 20MB;
int segment_id = shmget(IPC_PRIVATE, buffer_size, IPC_CREAT|IPC_EXCL|S_IRUSR|S_IWUSR); // allocate a shm segment
void* buf = shmat(segment_id, 0, 0); // attach

shmid_ds info;
shmtctl(segment_id, IPC_STAT, info); // check segment size
size_t segment_size = info.shm_segsz;

sprintf(buf, "hello message");

...
shmdt(buf); // detach, do not use buf after this
void* some_memory_address = 0x5000000;             // different address
buf = shmat(segment_id, some_memory_address, 0);   // reattach at a different address

...
shmdt(buf); // detach
shmctl(segment_id, IPC_RMID, 0); // deallocate shm segment
```

## Solarflare

### Example code

#### step 1 - setup
```cpp
// setup - open the driver, allocate protection domain, allocate virtual interface from the PD
ef_driver_handle driver_handle;
ef_vi vi;
ef_pd pd;

int ifindex;

ef_driver_open(&driver_handle);
ef_pd_alloc(&pd, driver_handle, ifindex, EF_PD_DEFAULT);
ef_vi_alloc_from_pd(&vi, driver_handle, &pd, driver_handle, -1, -1, -1, nullptr, -1, 0);
```

#### step 2 - create packet buffer
```cpp
// create packet buffer - allocate memory region and register it for packet buffers
const int BUF_SIZE = 2048;
int bytes = N_BUFS * BUF_SIZE;
void* p;
posix_memalign(&p, 4096, bytes);

ef_memreg memreg;
ef_memreg_alloc(&memreg, driver_handle, &pd, driver_handle, p, bytes);
```

#### step 2.1 - cache packet metadata
```cpp
#define MEMBER_OFFSET(c_type, mbr_name) ((uint32_t) (uintptr_t)(&((c_type*)0)->mbr_name))
#define CACHE_ALIGN __attribute__((aligned(EF_VI_DMA_ALIGN)))

struct pkt_buf {
  struct pkt_buf* next; /* We’re not actually going to use this; but chaining multiple buffers together is a common and useful trick. */
  ef_addr dma_buf_addr;
  int id;
  uint8_t dma_buf[1] CACHE_ALIGN; /* Not strictly required, but cache aligning the payload is a speed boost, so do it. */
};
/* We’re also going to want to keep track of all our buffers, so have an
array of them. Not strictly needed, but convenient. */
struct pkt_buf* pkt_bufs [N_BUFS];
for( i = 0; i < N_BUFS; ++i ) {
  pkt_buf* pb = (pkt_buf*) ((char*) p + i * 2048);
  pb->id = i;
  pb->dma_buf_addr = ef_memreg_dma_addr(&memreg, i * 2048);
  pb->dma_buf_addr += MEMBER_OFFSET(struct pkt_buf, dma_buf);
  pkt_bufs[i] = pb;
}
```

#### step 3 - add filters
```cpp
// add filters
struct sockaddr_in sa_local;
ef_filter_spec filter_spec;
ef_filter_spec_init(&filter_spec, EF_FILTER_FLAG_NONE);
ef_filter_spec_set_ip4_local(&filter_spec, IPPROTO_UDP, sa_local.sin_addr.s_addr, sa_local.sin_port);
ef_vi_filter_add(&vi, driver_handle, &filter_spec, nullptr);
```

#### step 4 - add packet buffers
```cpp
// push packet buffers to the rx descriptor ring
unsigned int rx_posted = 0;
int n;
for (int i = 0; i < n; ++i)
{
  struct pkt_buf* pb = pkt_bufs[rx_posted % N_RX_BUFS];
  ef_vi_receive_init(&vi, pb->dma_buf_addr, pb->id);
  ++rx_posted;
}
ef_vi_receive_push(&vi);
```

#### step 5 - handle packets
```cpp
// handle incoming packets, poll the event queue
ef_event evs[NUM_POLL_EVENTS];
int n_ev, i;

while (true) {
  n_ev = ef_eventq_poll(&vi, evs, NUM_POLL_EVENTS);
  if (n_ev > 0) {
    for ( i = 0; i < n_ev; ++i)
    {
      switch (EF_EVENT_TYPE(evs[i]))
      {
      case EF_EVENT_TYPE_RX:
        handle_rx_packet(EF_EVENT_RX_RQ_ID(evs[i]), EF_EVENT_RX_BYTES(evs[i]));
        break;
      case EF_EVENT_TYPE_RX_DISCARD:
        fprintf(stderr, "ERROR: RX_DISCARD type=%d", EF_EVENT_RX_DISCARD_TYPE(evs[i]));
        handle_rx_packet(EF_EVENT_RX_RQ_ID(evs[i]), EF_EVENT_RX_BYTES(evs[i]));
        break;
      }
    }
  }
}
```

#### step 6 - free resources
```cpp
/* Release and free a memory region */
int ef_memreg_free(ef_memreg* mr, ef_driver_handle mr_dh);

/* Release and free a virtual interface */
int ef_vi_free(ef_vi* vi, ef_driver_handle vi_dh);

/* Release and free a protection domain */
int ef_pd_free(ef_pd *pd, ef_driver_handle pd_dh);

/* close a driver handle */
int ef_driver_close(ef_driver_handle dh);
```

- TCP Direct: [https://docs.xilinx.com/v/u/en-US/SF-116303-CD-TCPDirect_User_Guide](https://docs.xilinx.com/v/u/en-US/SF-116303-CD-TCPDirect_User_Guide)
- EF_VI: [https://docs.xilinx.com/v/u/en-US/SF-114063-CD-ef_vi_User_Guide](https://docs.xilinx.com/v/u/en-US/SF-114063-CD-ef_vi_User_Guide)
- Documentation: [https://www.xilinx.com/support/download/nic-software-and-drivers.html#open](https://www.xilinx.com/support/download/nic-software-and-drivers.html#open)

## LMAX Disruptor

```cpp
class RingBuffer<E>;

```

```mermaid
---
title: LMAX
---
classDiagram
direction LR

class RingBuffer~E~

class EntryFactory

class Entry

class ProducerBarrier {
  + claim()
  + commit()
}

class ConsumerBarrier

class Consumer

class WaitStrategy

class BusySpinWaitStrategy
class YieldingWaitStrategy
class BlockingWaitStrategy

WaitStrategy <|-- BusySpinWaitStrategy
WaitStrategy <|-- YieldingWaitStrategy
WaitStrategy <|-- BlockingWaitStrategy

class ClaimStrategy

class SingleThreadedClaimStrategy
class MultiThreadedClaimStrategy

ClaimStrategy <|-- SingleThreadedClaimStrategy
ClaimStrategy <|-- MultiThreadedClaimStrategy
```

## Aeron Messaging
