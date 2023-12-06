# Competitive programming

## Header for C++ contests
```cpp
#include <bits/stdc++.h>

using namespace std;

using vi = vector<int>;
using vvi = vector<vi>;
using pii = pair<int, int>;
using vpii = vector<pii>;

#define rep(i,a,b) for(int i = (a); i < (b); ++i)
#define re(b) for(int lkzij = (b); lkzij > 0; --lkzij)
#define trav(a,x) for(auto& a : x)
#define all(x) begin(x), end(x)
#define sz(x) (int)(x).size()
```

## Rounding up to next integer value
```cpp
i = (val+k-1) / k;
```

## Uniform initialization
```cpp
struct Blah {
  vector<int> vi;
  Blah(std::initializer_list<int> l) : vi(l) {
    // ... l.size(), l.begin(), l.end()
  }
};

Blah b { 1, 2, 3 };

struct Foo {
  Foo(int a, int b) {}
};

Foo foo { 1, 2 };
```

## Copy into a vector
```cpp
#include <algorithm>
#include <iterator>

vector<int> src;
vector<int> dst;

copy(src.begin(), src.end(), back_inserter(dst));
```

## Print a vector
```cpp
#include <algorithm>
#include <iterator>

const char* separator;
vector<int> src;
copy(src.begin(), src.end(), ostream_iterator<int>(cout, separator));
```

## Thread
```cpp
#include <thread>

std::jthread t1(func, std::ref(obj1), val1);
t1.join();
```

## Async thread
```cpp
#include <future>
auto fut = async(std::launch::async, func, args, ...);
// func(args,...) will execute on a thread/thread-pool
fut.wait();
```

## Synchronization

### Mutex lock
```cpp
#include <mutex>
using namespace std;
mutex mut;
{                                   |  ~ +23 nsec
  lock_guard<mutex> guard(mut);     |  call pthread_mutex_lock(mut)
                                    |    if failed call __throw_system_error(...)
  ... critical section ...          |  ...
                                    |  call pthread_mutex_unlock(mut)
}
```

*Guarded* access to *shared* data is slow ... *unguarded* access to *non-shared* data is fast

### Atomic
```cpp
#include <atomic>
std::atomic<unsigned long> x(0);
unsigned long y(100);

{                                   |  ~ +7 nsec
  ++x; /* safe   */                 |  lock add DWORD PTR x[rip], 1  ; locks cache line
  ++y; /* unsafe */                 |  add DWORD PTR y[rip], 1
}
```

### Producer-Consumer
#### SPSC queue using atomic size (lock-free)
```cpp
array<Item, SIZE> Q;                |  // Q[0, N) is filled
atomic<size_t> N;                      // count of items
/* Producer */                      |  /* Consumer */
  produce(Q[N]);                       /* write after end of queue */
{                                   |  {
  ++N; /* advance end ptr */        |    while (N <= i) {}; /* wait for data */
}                                   |  }
                                    |  consume(Q[i]) // ok to use [0, N)
```

#### SPSC queue using locks
```cpp
array<Item, SIZE> Q;                |  // Q[0, N) is filled
size_t N;                              // count of items
mutex m;
/* Producer */                      |  /* Consumer */
  produce(Q[N]);                       /* write after end of queue */
{                                   |  {
  lock_guard l(m);                  |    size_t copy_of_N;
  ++N;                              |    do {
                                    |      lock_guard l(m);
                                    |      copy_of_N = N;
                                    |    } while (copy_of_N <= i);
}                                   |  }
                                    |  consume(Q[i]) // ok to use Q[0, N)
```

## Timeit
```cpp
#include <chrono>

auto tick = std::chrono::high_resolution_clock::now();
do_work();
auto tock = std::chrono::high_resolution_clock::now();
auto elapsed_secs = std::chrono::duration_cast<std::chrono::duration<double>>(tock - tick)).count();

// other clocks -- high_resolution_clock, system_clock
// system_clock -> measures realtime == wallclock time
// steady_clock -> monotonic clock
// high_resolution_clock -> system_clock (alias for smallest tick clock)
using std::chrono::{duration_cast, milliseconds, system_clock};
auto t0 = system_clock::now(); // system_clock::time_point
auto ms = duration_cast<milliseconds>(t1-t0).count();
```

## Old school time (nanosec granularity, high resolution)
```cpp
#include <time.h>
timespec real_ts0, proc_cpu_ts0, thread_cpu_ts0, monotonic_ts0;
clock_gettime(CLOCK_REALTIME, &real_ts0);
clock_gettime(CLOCK_PROCESS_CPUTIME_ID, &proc_cpu_ts0);
clock_gettime(CLOCK_THREAD_CPUTIME_ID, &thread_cpu_ts0);
clock_gettime(CLOCK_MONOTONIC_RAW, &monotonic_ts0);

secs(t) = t
nsecs(t) = t / 10**9
double duration(timespec a, timespec b) {
  return secs(a.tv_sec-b.tv_sec) + nsecs(a.tv_nsec-b.tv_nsec);
}
```

## Sleep in your code
```cpp
#include <unistd.h>
sleep(secs);
usleep(microsecs);

// --
#include <chrono>
#include <thread>

this_thread::sleep_for(chrono::milliseconds(msec));

using std::chrono_literals;
this_thread::sleep_for(400ms);

this_thread::sleep_until(steady_clock::now() + 500ms);
```

## Random data
```cpp
#include <random>

std::default_random_engine gen; // msvc: mt19937
std::uniform_int_distribution<int> U(1, 1000);
auto x_i = U(gen);

std::minstd_rand rgen; // minstd_rand0 minstd_rand mt19937 mt19937_64
const auto x_i = rgen();

std::random_device rd; // kernel random device
std::uniform_int_distribution<int> U(1, 1000);
auto x_i = U(rd);

std::random_device rd; // kernel random device
std::default_random_engine gen(rd()); // msvc: mt19937
std::uniform_int_distribution<int> U(1, 1000);
auto x_i = U(gen);

// seeded with time
std::default_random_engine gen(time(0));
auto X = gen();

// old school
#include <cstdlib>
#include <ctime>

srand(time(0)); // seed with time
srand(0); // seed with a deterministic value
int X = rand();
```

## Generate N random strings of lengths upto L
```cpp
constexpr uint L = 2**22, N = 2**18;
constexpr ntimes = 2**10;

// generate 1 random string of length
unique_ptr<char[]> s = new char[L];
memset(s.get(), 'a', L*sizeof(char));
for (uint i = 0; i < ntimes; ++i)
{
  s[rgen() % (L-1)] = 'a' + (rgen() % 26);
}
s[L-1] = 0;

// fill a vector of pointers starting at random index in s
vector<const char*> vs(N);
for (uint i = 0; i < N; ++i)
{
  vs[i] = &s[rgen() % (L-1)];
}
```

## Generate N random ints
```cpp
#include <algorithm>
for (size_t i = 0; i < N; ++i) { v[i] = i;}
std::random_shuffle(v.begin(), v.end());
```

## Use array of function pointers to avoid branch
```cpp
ulong f1(ulong x, ulong y);
ulong f2(ulong x, ulong y);

decltype(f)* fp[] = { f1, f2 };
bool* flag = new bool[...];
for (int i = 0; i < N; ++i) {
  a += f[flag[i]](p1[i], p2[i]);
}

--- equivalent ---
  a += f[flag[i]](p1[i], p2[i]);           // cons: no inlining possible

  if (flag[i]) { a += f1(p1[i], p2[i]); }
  else         { a += f2(p1[i], p2[i]); }
```

## Use lookup table
```cpp
#define times(i,N) for (int i = 0; i < N; ++i)

unsigned char* c = ...;  // random values in [0, 255]
unsigned char LUT[256] = { 0, 1, ..., 127, 128, 128, ..., 128 };
times(i,N) {
  c[i] = LUT[c[i]];
}

--- equivalent ---
  c[i] = LUT[c[i]];

  c[i] = (c[i] < 128) ? c[i] : 128;
```

## Avoid branches
```cpp
ulong a1 = 0, a2 = 0;
ulong* a[2] = { &a2, &a1 };
times(i,N) {
  ulong s[2] = { p1[i]*p2[i], p1[i]-p2[i] };
  a[b1[i]] += s[b1[i]];
}

--- or ---

ulong a1 = 0, a2 = 0;
times(i,N) {
  ulong s1[2] = { 0, p1[i]-p2[i] };
  ulong s2[2] = { p1[i]*p2[i], 0 };
  a1 += s1[b1[i]];
  a2 += s2[b1[i]];
}

--- equivalent to ---
times(i,N) {
  if (b1[i]) {
    a1 = p1[i]-p2[i];
  }
  else {
    a2 = p1[i]*p2[i];
  }
}
```

## Build Benchmark, GTest
```shell
# build google benchmark
cmake google-benchmark -B build-release \
    -DCMAKE_BUILD_TYPE=Release \
    -DBENCHMARK_DOWNLOAD_DEPENDENCIES=on  \
    -DCMAKE_BUILD_TYPE=Release  \
    -DCMAKE_INSTALL_PREFIX=d:/devtools/benchmark  \

cmake --build build-release --config Release
ctest --build-config Release
cmake --build . --config Release --target install

# build google test
cmake google-benchmark\googletest -B googletest-release \
    -DCMAKE_INSTALL_PREFIX=d:/devtools/google-test \
    -DBUILD_GMOCK=OFF \
    -Dgtest_force_shared_crt=on \

cmake --build googletest-release --config Release
cmake --build googletest-release --config Release --target install

# build project using these
cmake . -B build-msvc \
    -GNinja \
    -DCMAKE_BUILD_TYPE=Release \
    -Dbenchmark_ROOT=d:/devtools/benchmark \
    -DGTest_ROOT=d:/devtools/google-test \

cmake --build build-msvc
```

### Use google benchmark
```cpp
#include <benchmark/benchmark.h>

void BM_some_name(benchmark::State& state) {
  // args passed to BM are in state.range(i)
  // state.range(0) == 100
  ... init ..
  for (auto _ : state) {
    ... code to measure ...
    benchmark::DoNotOptimize(someFuncToMeasure(...));
  }
}
BENCHMARK(BM_some_name)->Arg(100); // Arg -> state.range(i)

...

BENCHMARK_MAIN();

// c++ -g  ... -lbenchmark -pthread
// cmake target_link_libraries(... benchmark::benchmark)

// cl.exe /nologo /TP \
//     -DBENCHMARK_STATIC_DEFINE \
//     -external:I${benchmark_ROOT}/include \
//     -external:W0 \
//     /DWIN32 \
//     /D_WINDOWS \
//     /EHsc \
//     /O2 \
//     /Ob2 \
//     /DNDEBUG \
//     -std:c++20 \
//     -MD \
//     /showIncludes \
//     /Foobjdir/blah.obj \
//     /Fdobjdir/ \
//     /FS \
//     -c \
//     blah.cpp

// vs_link_exe --rc="...\rc.exe" \
//     --mt="...\mt.exe" \
//     --manifests \
//     -- \
//     ...\link.exe \
//     /nologo \
//     objdir/blah.obj \
//     /out:blah.exe \
//     /implib:blah.lib \
//     /pdb:blah.pdb \
//     /version:0.0 \
//     /machine:x64 \
//     /INCREMENTAL:NO \
//     /subsystem:console \
//     ${benchmark_ROOT}\lib\benchmark.lib \
//     shlwapi.lib \
//     kernel32.lib \
//     user32.lib \
//     gdi32.lib \
//     winspool.lib \
//     shell32.lib \
//     ole32.lib \
//     oleaut32.lib \
//     uuid.lib \
//     comdlg32.lib \
//     advapi32.lib

```

## Backup
```text
pushd C:\Program Files
7z a z:\files-for-vm\vs2.7z "Microsoft Visual Studio\2022\Community" dotnet
pushd C:\Program Files (x86)
7z a z:\files-for-vm\vs3.7z dotnet "Microsoft SDKs" "Windows Kits" MSBuild Microsoft.NET "Microsoft Visual Studio"
```

## Tools of trade
- Google benchmark, catch2, nanobenchmark
- Google test, doctest
- Google profiler
- LLVM Machine Code Analyzer (LLVM MCA), look at timeline for assembly code execution
- renatoGarcia/icecream-cpp

## Visual Studio C++ Dirs
```text
-- cmake, ninja --
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin\cmake.exe
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\Ninja\ninja.exe

-- Developer Command Prompt
%comspec% /k "C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\Tools\VsDevCmd.bat"

-- x64 Native Tools Command Prompt
%comspec% /k "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvars64.bat"

-- x64_x86 Cross Tools Command Prompt for VS 2022
%comspec% /k "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsamd64_x86.bat"

-- x86 Native Tools Command Prompt for VS 2022
%comspec% /k "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvars32.bat"

-- x86_x64 Cross Tools Command Prompt for VS 2022
%comspec% /k "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsx86_amd64.bat"


set VS_ROOT=C:\Program Files\Microsoft Visual Studio\2022\Community
set WINKITS=C:\Program Files (x86)\Windows Kits

set PATH+=;%VS_ROOT%\VC\Redist\MSVC\14.38.33130\debug_nonredist\x64\Microsoft.VC143.DebugCRT
 - or -
set PATH+=;\VC\Redist\MSVC\14.38.33130\x64\Microsoft.VC143.CRT
set PATH+=;\VC\Tools\MSVC\14.38.33130\bin\HostX64\x64

set PATH+=;%WINKITS%\10\bin\10.0.22621.0\x64\ucrt
set PATH+=;%WINKITS%\10\bin\10.0.22621.0\x64

-- important directories in path --
C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\bin\HostX86\x86
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\VC\VCPackages
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\TestWindow
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\TeamFoundation\Team Explorer
C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\bin\Roslyn
C:\Program Files\Microsoft Visual Studio\2022\Community\Team Tools\Performance Tools
C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\FSharp\Tools
C:\Program Files\Microsoft Visual Studio\2022\Community\Team Tools\DiagnosticsHub\Collector
C:\Program Files (x86)\Windows Kits\10\bin\10.0.22621.0\x86
C:\Program Files (x86)\Windows Kits\10\bin\x86
C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\amd64
C:\Windows\Microsoft.NET\Framework\v4.0.30319
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\Tools
C:\Windows\system32
C:\Windows
C:\Windows\System32\Wbem
C:\Windows\System32\WindowsPowerShell\v1.0
C:\Windows\System32\OpenSSH
C:\Program Files\Microsoft SQL Server\150\Tools\Binn
C:\Program Files\dotnet
C:\Program Files (x86)\Windows Kits\10\Windows Performance Toolkit
C:\Users\User\AppData\Local\Microsoft\WindowsApps
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\Ninja
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\VC\Linux\bin\ConnectionManagerExe
C:\Program Files\Microsoft Visual Studio\2022\Community\VC\vcpkg

-- the env --
ALLUSERSPROFILE=C:\ProgramData
APPDATA=C:\Users\User\AppData\Roaming
CommandPromptType=Native
CommonProgramFiles=C:\Program Files\Common Files
CommonProgramFiles(x86)=C:\Program Files (x86)\Common Files
CommonProgramW6432=C:\Program Files\Common Files
COMPUTERNAME=WINDEV2311EVAL
ComSpec=C:\Windows\system32\cmd.exe
DevEnvDir=C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\
DriverData=C:\Windows\System32\Drivers\DriverData
EFC_5140=1
ExtensionSdkDir=C:\Program Files (x86)\Microsoft SDKs\Windows Kits\10\ExtensionSDKs
EXTERNAL_INCLUDE=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\include;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\ATLMFC\include;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\VS\include;C:\Program Files (x86)\Windows Kits\10\include\10.0.22621.0\ucrt;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\um;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\shared;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\winrt;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\cppwinrt;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.8\include\um
Framework40Version=v4.0
FrameworkDir=C:\Windows\Microsoft.NET\Framework\
FrameworkDir32=C:\Windows\Microsoft.NET\Framework\
FrameworkVersion=v4.0.30319
FrameworkVersion32=v4.0.30319
FSHARPINSTALLDIR=C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\FSharp\Tools
HOMEDRIVE=C:
HOMEPATH=\Users\User
INCLUDE=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\include;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\ATLMFC\include;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\VS\include;C:\Program Files (x86)\Windows Kits\10\include\10.0.22621.0\ucrt;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\um;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\shared;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\winrt;C:\Program Files (x86)\Windows Kits\10\\include\10.0.22621.0\\cppwinrt;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.8\include\um
LIB=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\ATLMFC\lib\x86;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\lib\x86;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.8\lib\um\x86;C:\Program Files (x86)\Windows Kits\10\lib\10.0.22621.0\ucrt\x86;C:\Program Files (x86)\Windows Kits\10\\lib\10.0.22621.0\\um\x86
LIBPATH=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\ATLMFC\lib\x86;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\lib\x86;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\lib\x86\store\references;C:\Program Files (x86)\Windows Kits\10\UnionMetadata\10.0.22621.0;C:\Program Files (x86)\Windows Kits\10\References\10.0.22621.0;C:\Windows\Microsoft.NET\Framework\v4.0.30319
LOCALAPPDATA=C:\Users\User\AppData\Local
LOGONSERVER=\\WINDEV2311EVAL
NETFXSDKDir=C:\Program Files (x86)\Windows Kits\NETFXSDK\4.8\
NUMBER_OF_PROCESSORS=4
OneDrive=C:\Users\User\OneDrive
OS=Windows_NT
Path=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\bin\HostX86\x86;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\VC\VCPackages;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\TestWindow;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\TeamFoundation\Team Explorer;C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\bin\Roslyn;C:\Program Files\Microsoft Visual Studio\2022\Community\Team Tools\Performance Tools;C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools\;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\FSharp\Tools;C:\Program Files\Microsoft Visual Studio\2022\Community\Team Tools\DiagnosticsHub\Collector;C:\Program Files (x86)\Windows Kits\10\bin\10.0.22621.0\\x86;C:\Program Files (x86)\Windows Kits\10\bin\\x86;C:\Program Files\Microsoft Visual Studio\2022\Community\\MSBuild\Current\Bin\amd64;C:\Windows\Microsoft.NET\Framework\v4.0.30319;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\Tools\;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files\Microsoft SQL Server\150\Tools\Binn\;C:\Program Files\dotnet\;C:\Program Files (x86)\Windows Kits\10\Windows Performance Toolkit\;C:\Users\User\AppData\Local\Microsoft\WindowsApps;;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\Ninja;C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\VC\Linux\bin\ConnectionManagerExe;C:\Program Files\Microsoft Visual Studio\2022\Community\VC\vcpkg
PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
PROCESSOR_ARCHITECTURE=AMD64
PROCESSOR_IDENTIFIER=Intel64 Family 6 Model 167 Stepping 1, GenuineIntel
PROCESSOR_LEVEL=6
PROCESSOR_REVISION=a701
ProgramData=C:\ProgramData
ProgramFiles=C:\Program Files
ProgramFiles(x86)=C:\Program Files (x86)
ProgramW6432=C:\Program Files
PROMPT=$P$G
PSModulePath=C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules
PUBLIC=C:\Users\Public
SESSIONNAME=Console
SystemDrive=C:
SystemRoot=C:\Windows
TEMP=C:\Users\User\AppData\Local\Temp
TMP=C:\Users\User\AppData\Local\Temp
UCRTVersion=10.0.22621.0
UniversalCRTSdkDir=C:\Program Files (x86)\Windows Kits\10\
USERDOMAIN=WINDEV2311EVAL
USERDOMAIN_ROAMINGPROFILE=WINDEV2311EVAL
USERNAME=User
USERPROFILE=C:\Users\User
VCIDEInstallDir=C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\VC\
VCINSTALLDIR=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\
VCPKG_ROOT=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\vcpkg
VCToolsInstallDir=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.38.33130\
VCToolsRedistDir=C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Redist\MSVC\14.38.33130\
VCToolsVersion=14.38.33130
VisualStudioVersion=17.0
VS170COMNTOOLS=C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\Tools\
VSCMD_ARG_app_plat=Desktop
VSCMD_ARG_HOST_ARCH=x86
VSCMD_ARG_TGT_ARCH=x86
VSCMD_VER=17.8.2
VSINSTALLDIR=C:\Program Files\Microsoft Visual Studio\2022\Community\
windir=C:\Windows
WindowsLibPath=C:\Program Files (x86)\Windows Kits\10\UnionMetadata\10.0.22621.0;C:\Program Files (x86)\Windows Kits\10\References\10.0.22621.0
WindowsSdkBinPath=C:\Program Files (x86)\Windows Kits\10\bin\
WindowsSdkDir=C:\Program Files (x86)\Windows Kits\10\
WindowsSDKLibVersion=10.0.22621.0\
WindowsSdkVerBinPath=C:\Program Files (x86)\Windows Kits\10\bin\10.0.22621.0\
WindowsSDKVersion=10.0.22621.0\
WindowsSDK_ExecutablePath_x64=C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools\x64\
WindowsSDK_ExecutablePath_x86=C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools\
__DOTNET_ADD_32BIT=1
__DOTNET_PREFERRED_BITNESS=32
__VSCMD_PREINIT_PATH=C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files\Microsoft SQL Server\150\Tools\Binn\;C:\Program Files\dotnet\;C:\Program Files (x86)\Windows Kits\10\Windows Performance Toolkit\;C:\Users\User\AppData\Local\Microsoft\WindowsApps;

```

## Buzz words
- New SSE 4.2 Instructions
- Improved Lock Support
- Additional Caching Hierarchy
- Deeper Buffers
- Simultaneous Multi-threading
- Faster Virtualization
- Better Branch Prediction
- Improved Loop Streaming
- Execution Unit
- L1 Data Cache
- Memory Order & Execution
- L2 Cache & Interrupt Servicing
- Paging
- Branch Prediction
- Out-of-order Scheduling & Retirement
- Instruction Decode & Microcode
- Instruction Fetch & L1 Cache

# Glossary
- CPU
  - Instruction Level Parallelism (ILP) - if operands are already in registers, CPU can execute several operations at once (77)
  - Pipelining - a complex exporession is broken into stages and executed in a pipeline. Stage 2 of previous expression runs at the same time as stage 1 of next one (83)
  - Register renaming (85)
  - Loop unrolling
  - Conditional Move/Add instructions to avoid conditional jump screwing up pipeline (88)
  - Branch prediction - CPU analyzes history of every branch in the code and assumes behavior will not change (92)
  - Speculative execution - execute code before we know for sure whether that branch will be taken or not (92)
  - Pipeline flush - expensive, prediction was wrong, discard the result of every instruction that should not have been evaluated (92)
  - Branch misprediction - profile with gperf
  - Branchless computing (103)
  - Loop Unrolling
  - Branchless selection
- Memory
  - Column Access Strobe Latency / CAS Latency / CL - num of cycles for RAM to recv + process + return value for a data request (116)
  - cache hierarchy (CPU - L1 - L2 - L3 - RAM)
  - SRAM (cache, faster, more electricity) vs DRAM (RAM, slower, less power consumed)
  - L1 48KB (per-core), L2 512KB (per-core), L3 16MB (per-cpu)
  - Cache Hit (good), Cache Miss (slow)
  - Latency - delay between time of request for data issued and time data is retrieved
  - Bandwidth - amount of data memory bus can transmit a given time
  - Prefetch - forward/backward access orders detected, fetch with stride (skip k items) detected

# Latency numbers

| Operation | Time | Size | | Cycle |
|---|---|---|---|---|
| CPU instruction cycle | 0.4 ns || 2.5 GHz | 1 cycle |
| CPU registers | ||||
| L1 cache | 0.5-1 ns | 48KB | SRAM | 4-5 cycles |
| Branch misprediction| 3-5 ns ||||
| L2 cache | 4-7 ns | 512KB | SRAM| 13 cycles |
| Mutex lock/unlock | 17-25 ns ||||
| L3 Cache || 16MB || 42 cycles |
| RAM | 100 ns| 32GB | DRAM| 42 cycles + 70 nsec |
| PCIe card to RAM (DMA) |||| ? |
| Compress 1KB w/Zippy | 3us ||||
| Send 2KB over 1Gbps nw| 20us ||||
| SSD random read | 150us ||||
| Read 1MB seq from RAM | 250us ||||
| Roundtrip within same datacenter| 0.5ms ||||
| Read 1MB seq from SSD | 1ms ||||
| Disk seek | 10ms ||||
| Read 1MB seq from disk | 20ms ||||

Source: [Latency Numbers Everyone Should Know](https://static.googleusercontent.com/media/sre.google/en//static/pdf/rule-of-thumb-latency-numbers-letter.pdf)
Ice Lake: [CPU Benchmark](https://www.7-cpu.com/cpu/Ice_Lake.html)

