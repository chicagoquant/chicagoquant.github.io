# Competitive programming

- [Competitive programming](#competitive-programming)
  - [Header for C++ contests](#header-for-c-contests)
  - [Canonical Class](#canonical-class)
    - [Overloads with ref-qualifier](#overloads-with-ref-qualifier)
    - [Copy-Move-Swap Idioms](#copy-move-swap-idioms)
    - [Lazy Initialization](#lazy-initialization)
  - [Dump predefined macros](#dump-predefined-macros)
  - [Watch memory allocation](#watch-memory-allocation)
  - [Rounding up to next integer value](#rounding-up-to-next-integer-value)
  - [Uniform initialization](#uniform-initialization)
  - [Copyable Moveable](#copyable-moveable)
  - [Method chaining](#method-chaining)
  - [Copy into a vector](#copy-into-a-vector)
    - [Copying](#copying)
  - [CPP Features](#cpp-features)
    - [CPP Data Types](#cpp-data-types)
    - [CPP Number limits](#cpp-number-limits)
    - [Function pointers](#function-pointers)
    - [CPP File IO](#cpp-file-io)
      - [CPP CSV Files](#cpp-csv-files)
      - [fstream](#fstream)
    - [Structured binding](#structured-binding)
    - [Swap](#swap)
  - [Crazy STL](#crazy-stl)
    - [Smart Pointers](#smart-pointers)
    - [enable if](#enable-if)
      - [Usage - 4 ways](#usage---4-ways)
    - [any, variant, optional](#any-variant-optional)
      - [Usage - any (type-safe void\*)](#usage---any-type-safe-void)
      - [Implementation idea - any](#implementation-idea---any)
      - [Usage - variant (type-safe union)](#usage---variant-type-safe-union)
      - [Implementation idea - variant](#implementation-idea---variant)
      - [Usage - optional](#usage---optional)
      - [Implementation idea - optional](#implementation-idea---optional)
    - [Tag Dispatch](#tag-dispatch)
    - [Type Erasure](#type-erasure)
    - [CRTP](#crtp)
    - [Return type resolver](#return-type-resolver)
    - [virtual constructor idiom](#virtual-constructor-idiom)
    - [std string\_view](#std-string_view)
    - [std span](#std-span)
    - [std function](#std-function)
    - [lambda expanded](#lambda-expanded)
    - [Using lambdas](#using-lambdas)
    - [Class Template Argument Deduction (CTAD)](#class-template-argument-deduction-ctad)
    - [std bind](#std-bind)
    - [sort](#sort)
    - [sum of vector](#sum-of-vector)
    - [std ranges](#std-ranges)
    - [Utilities - move forward](#utilities---move-forward)
  - [Templates](#templates)
    - [Variadic Template Function](#variadic-template-function)
    - [Variadic Template Class](#variadic-template-class)
    - [Abbreviated function template, placeholder types](#abbreviated-function-template-placeholder-types)
    - [template auto](#template-auto)
  - [Concepts](#concepts)
    - [Very simple example](#very-simple-example)
  - [Print type name](#print-type-name)
    - [have compiler spit out the type name](#have-compiler-spit-out-the-type-name)
    - [utility function for printing type name](#utility-function-for-printing-type-name)
  - [RAII for malloc/free](#raii-for-mallocfree)
  - [Print a vector](#print-a-vector)
  - [Thread](#thread)
  - [Async thread](#async-thread)
  - [Synchronization](#synchronization)
    - [Mutex lock](#mutex-lock)
      - [Read-Write lock](#read-write-lock)
    - [Atomic](#atomic)
      - [Atomic for 2 numbers, pack them in 64-bit atomic word](#atomic-for-2-numbers-pack-them-in-64-bit-atomic-word)
    - [Spinlock (not optimized, not good performance)](#spinlock-not-optimized-not-good-performance)
      - [A bit better, but still not great](#a-bit-better-but-still-not-great)
      - [Optimized spin-lock](#optimized-spin-lock)
      - [Read Write Spinlock](#read-write-spinlock)
    - [Spinlock to control access to an object](#spinlock-to-control-access-to-an-object)
    - [Atomic counter, array next empty slot index](#atomic-counter-array-next-empty-slot-index)
    - [Thread Safe Unique Pointer](#thread-safe-unique-pointer)
    - [Thread Safe Shared Pointer](#thread-safe-shared-pointer)
    - [Producer-Consumer](#producer-consumer)
      - [SPSC queue using atomic size (lock-free, wait-free)](#spsc-queue-using-atomic-size-lock-free-wait-free)
      - [SPSC queue using locks](#spsc-queue-using-locks)
    - [Memory order](#memory-order)
      - [SPSC queue using atomic size (lock-free, wait-free, with appropriate memory order)](#spsc-queue-using-atomic-size-lock-free-wait-free-with-appropriate-memory-order)
      - [Release order](#release-order)
      - [Acquire order](#acquire-order)
    - [Compare and swap CAS (lock-free, but not wait-free)](#compare-and-swap-cas-lock-free-but-not-wait-free)
      - [Multiply operation in assembly is not atomic](#multiply-operation-in-assembly-is-not-atomic)
  - [Thread-safe Singleton, Double checked locking](#thread-safe-singleton-double-checked-locking)
  - [Data Strucutures](#data-strucutures)
    - [Thread safe stack](#thread-safe-stack)
      - [Problematic interface](#problematic-interface)
      - [Better interface](#better-interface)
      - [Locked stack](#locked-stack)
    - [Thread Safe Queue](#thread-safe-queue)
      - [Option 1 -- spinlock](#option-1----spinlock)
      - [Option 2 -- lock-free, wait-free queue SPSC (1 producer, 1 consumer)](#option-2----lock-free-wait-free-queue-spsc-1-producer-1-consumer)
  - [Coroutines in C++20](#coroutines-in-c20)
    - [Bare c++](#bare-c)
  - [Timeit](#timeit)
  - [Old school time (nanosec granularity, high resolution)](#old-school-time-nanosec-granularity-high-resolution)
  - [Sleep in your code](#sleep-in-your-code)
  - [Random data](#random-data)
  - [Generate N random strings of lengths upto L](#generate-n-random-strings-of-lengths-upto-l)
  - [Generate N random ints](#generate-n-random-ints)
  - [Use array of function pointers to avoid branch](#use-array-of-function-pointers-to-avoid-branch)
  - [Use lookup table](#use-lookup-table)
  - [Avoid branches](#avoid-branches)
  - [Build Benchmark, GTest](#build-benchmark-gtest)
    - [Use google benchmark](#use-google-benchmark)
  - [Build Catch2 unittests](#build-catch2-unittests)
    - [Catch2 - Build local copies from GIT repo](#catch2---build-local-copies-from-git-repo)
    - [Catch2 - Example CMakeLists.txt file](#catch2---example-cmakeliststxt-file)
    - [Catch2 - Build your code](#catch2---build-your-code)
    - [Catch2 - Example test code](#catch2---example-test-code)
  - [Backup](#backup)
  - [Tools of trade](#tools-of-trade)
  - [Visual Studio C++ Dirs](#visual-studio-c-dirs)
  - [Buzz words](#buzz-words)
  - [Glossary](#glossary)
  - [Latency numbers](#latency-numbers)
    - [Create Shortcut on windows](#create-shortcut-on-windows)
- [Command line](#command-line)
    - [Zoxide](#zoxide)
    - [Start VM](#start-vm)
    - [Export GIT repository](#export-git-repository)
    - [Readonly GIT repository](#readonly-git-repository)
    - [MinTTY Terminal Bash](#mintty-terminal-bash)
    - [Veracrypt](#veracrypt)
    - [Music download](#music-download)
- [Systems Programming](#systems-programming)
  - [Memory](#memory)
    - [Virtual Memory](#virtual-memory)
    - [Shared memory Anonymous](#shared-memory-anonymous)
    - [Shm Named File](#shm-named-file)
    - [Shared memory segment IPC](#shared-memory-segment-ipc)
  - [Solarflare](#solarflare)
    - [Example code](#example-code)
      - [step 1 - setup](#step-1---setup)
      - [step 2 - create packet buffer](#step-2---create-packet-buffer)
      - [step 2.1 - cache packet metadata](#step-21---cache-packet-metadata)
      - [step 3 - add filters](#step-3---add-filters)
      - [step 4 - add packet buffers](#step-4---add-packet-buffers)
      - [step 5 - handle packets](#step-5---handle-packets)
      - [step 6 - free resources](#step-6---free-resources)
  - [LMAX Disruptor](#lmax-disruptor)
  - [Aeron Messaging](#aeron-messaging)
- [Design Patterns](#design-patterns)
  - [DP - Creational - Factory Method - Identifier](#dp---creational---factory-method---identifier)
  - [DP - Creational - Factory Method - Inheritance](#dp---creational---factory-method---inheritance)
  - [DP - Creational - Abstract Factory](#dp---creational---abstract-factory)
  - [DP - Creational - Builder](#dp---creational---builder)
  - [DP - Creational - Prototype](#dp---creational---prototype)
  - [DP - Creational - Singleton](#dp---creational---singleton)
  - [DP - Creational - RAII](#dp---creational---raii)
  - [DP - Creational - Object Pool](#dp---creational---object-pool)
  - [DP - Creational - Multiton](#dp---creational---multiton)
  - [DP - Creational - Lazy Initialization](#dp---creational---lazy-initialization)
  - [DP - Creational - Dependency Injecton](#dp---creational---dependency-injecton)
  - [DP - Structural - Adapter](#dp---structural---adapter)
  - [DP - Structural - Bridge](#dp---structural---bridge)
  - [DP - Structural - Composite](#dp---structural---composite)
  - [DP - Structural - Decorator](#dp---structural---decorator)
  - [DP - Structural - Facade](#dp---structural---facade)
  - [DP - Structural - Flyweight](#dp---structural---flyweight)
  - [DP - Structural - Proxy](#dp---structural---proxy)
  - [DP - Behaviroal - Chain of responsibility](#dp---behaviroal---chain-of-responsibility)
  - [DP - Behaviroal - Command](#dp---behaviroal---command)
  - [DP - Behaviroal - Interpreter](#dp---behaviroal---interpreter)
  - [DP - Behaviroal - Iterator](#dp---behaviroal---iterator)
  - [DP - Behaviroal - Mediator](#dp---behaviroal---mediator)
  - [DP - Behaviroal - Memento](#dp---behaviroal---memento)
  - [DP - Behaviroal - Observer](#dp---behaviroal---observer)
  - [DP - Behaviroal - State](#dp---behaviroal---state)
  - [DP - Behaviroal - Strategy](#dp---behaviroal---strategy)
  - [DP - Behaviroal - Template method](#dp---behaviroal---template-method)
  - [DP - Behaviroal - Visitor](#dp---behaviroal---visitor)
  - [SOLID](#solid)
  - [Design goals](#design-goals)

---

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

Lots of headers [Open this in Wandbox](https://wandbox.org/permlink/BiJDPA9v1OQqhHzo)
```cpp
#include <iostream>
#include <variant>
#include <vector>
#include <map>
#include <string>
#include <type_traits>
#include <utility>
#include <algorithm>
#include <functional>
#include <memory>
#include <cstdint>
#include <cstdlib>
#include <numeric>
#include <mutex>
#include <thread>
#include <optional>
#include <sstream>
#include <string_view>
#include <iomanip>                  // for quoted(str)
#include <boost/core/demangle.hpp>

#include <ranges>

namespace rs = std::ranges;
namespace rv = std::ranges::views;   // same as std::views

using namespace std;
using namespace std::string_literals;   // for "..."s

#pragma GCC diagnostic ignored "-Wunused-parameter"
#pragma GCC diagnostic ignored "-Wunused-variable"

auto print_elem = [](auto const e) {std::cout << e << '\n'; };

int main([[maybe_unused]]int argc, [[maybe_unused]] const char* argv[])
{
    auto s = "hello"s;
    cout << s << endl;
    cout << string(100, '-') << endl;
}

// flag: -Wno-unused
```

## Canonical Class

```cpp
#include <iostream>

using namespace std;

class A {
public:
  // default
  A() { cout << "A::default ctor(this=" << this << ")\n"; }
  ~A() { cout << "A::dtor(this=" << this << ")\n"; }
  A(A const& rhs) { cout << "A::copy ctor(this=" << this << ", const A& rhs=" << &rhs << ")\n"; }
  A(A&& rhs) noexcept { cout << "A::move ctor(this=" << this << ", A&& rhs=" << &rhs << ")\n"; }

  // A& operator=(A const& rhs) { cout << "A::copy assignment(this=" << this << ") = " << &rhs << "\n"; return *this; }
  // A& operator=(A&& rhs) noexcept { cout << "A::move assignment(this=" << this << ") = " << &rhs << "\n"; rhs.swap(*this); return *this; }

  // replaces above 2 assignment operators
  A& operator=(A rhs) noexcept { cout << "A::copy_val assignment(this=" << this << ") = " << &rhs << "\n"; swap(*this, rhs); return *this; }

  // replaces both A::swap(b), std::swap(a, b)
  friend void swap(A& a, A& b) noexcept {
    cout << "friend swap(A& a=" << &a << ", A& b=" << &b << ")" << endl;
    // member1.swap(b.member1); or std::swap(a.member, b.member);
    // swap(pointerMember, b.pointerMember);
    // swap(basicTypeMember, b.basicTypeMember);
  }

  // void swap(A& b) noexcept {
  //   cout << "A::swap(this=" << this << ", A& b=" << &b << ")" << endl;
  //   // member1.swap(b.member1); or std::swap(a.member, b.member);
  //   // swap(pointerMember, b.pointerMember);
  //   // swap(basicTypeMember, b.basicTypeMember);
  // }
};

// namespace std {
//   // non-member swap, if we don't define, then default implementation will do tmp-move(a)-move(b)-move(tmp)
//   template<>                           // full-specialization required if defininig in std namespace
//   void swap(A& a, A& b) noexcept {
//     a.swap(b);
//   }
// }

class B : public A {
public:
  B() { cout << "B::default ctor(this=" << this << ")\n"; }
  ~B() { cout << "B::dtor(this=" << this << ")\n"; }

  void foo() { cout << "B::foo(this=" << this << ")\n"; }
};
```

Initializations: aggregate, constant, copy, default, direct, list, reference, value, zero

```cpp
T t = { 'a', "hello", 1, }; // aggregate
const int T::a = 5; // constant, static const member
T copy_t = t; // copy
T t; new T; // default
T t(some_param); // direct
T t { 'a', "hello", 1 }; // list
T& tr = t; // reference
T t = T(); T{};  // value (empty-initializer)
static T t; T t(); // zero
```

### Overloads with ref-qualifier

Overloads of class function -- ref, const-ref, rvalue, const-rvalue
```cpp
template<typename T>
class X {
  constexpr T&        get_value() &       { return get_value_impl(*this); }
  constexpr const T&  get_value() const&  { return get_value_impl(*this); }
  constexpr T&&       get_value() &&      { return get_value_impl(move(*this)); }
  constexpr const T&& get_value() const&& { return get_value_impl(move(*this)); }

  template<typename Opt>
  static decltype(auto) get_value_impl(Opt&& opt) {
    return forward<Opt>(opt).val_;
  }
  T val_;
};

// better, with C++23
template<typename T>
class X {
  template<typename Self>
  constexpr auto&& get_value(this Self&& self) {  // not valid before C++23
    return forward<Self>(self).val_;
  }
  T val_;
};
```

### Copy-Move-Swap Idioms
```cpp
class A
{
  Big big;
  Pointer* ptr;
  int v;
public:
  A(const A& that) : big(that.big), ptr(nullptr), v(that.v) {
    ptr = new Pointer(*that.ptr);
  }

  A(A&& other) : big(std::move(other.big)), ptr(exchange(other.ptr, nullptr)), v(other.v) noexcept {
  }

  // replaces both copy and move assignment operators: operator=(const A&), operator=(A&&)
  A& operator=(A that) noexcept {      // create a copy
    that.swap(*this);         // swap the copy
    return *this;
  }

  ~A() {
    delete ptr;
  }

  // A& operator=(const A& other) {
  //   if (this != &other) {
  //     A tmp(other);
  //     tmp.swap(*this);
  //   }
  //   return *this;
  // }
  //
  // A& operator=(A&& other) noexcept {
  //   other.swap(*this);
  //   return *this;
  // }

  // if we don't define, then default implementation will do tmp-move(a)-move(b)-move(tmp)
  friend void swap(A& a, A& b) noexcept {  // note: not defining member swap, just using friend non-member swap
    using std::swap;
    swap(a.big, b.big);
    swap(a.ptr, b.ptr);
    swap(a.v, b.v);
  }
};
```

### Lazy Initialization

```cpp
// option 1: Using std optional -- object on stack
class Lazy
{
  optional<BigObject> big{};
public:
  void eval_lazy() {
    if (!big) {                             // no thread-safety
      big.emplace(...);                     // lazily construct big
    }
    big->some_method(...);
  }
};

// option 2: Using std smart pointer -- object created on heap
class Lazy
{
  unique_ptr<BigObject> big{};
public:
  void eval_lazy() {
    if (!big) {                             // no thread-safety
      big = make_unique<BigObject>(...);    // lazily construct big
    }
    big->some_method(...);
  }
};

// source: https://www.cppstories.com/2019/10/lazyinit/

// option 3: Using raw pointer -- forced to implement dtor, and rule-of-seven or rule-of-five
// class Lazy
// {
//   BigObject* big {nullptr};
// public:
//   ~Lazy() { delete big;  }
//   // have to implment all ctors
//   void eval_lazy() {
//     if (!big) {
//       big = new BigObject {...};           // lazily construct big
//     }
//     big->some_method(...);
//   }
// };

class ThreadSafeLazy : public Lazy
{
  mutable mutex mut;    // not copyable, not movable, need custom copy ctors, assignment etc
public:

  ThreadSafeLazy(const ThreadSafeLazy& other) noexcept { /* do not copy mut, copy the rest */ big = other.big; }
  ThreadSafeLazy& operator=(const ThreadSafeLazy& other) noexcept { /* do not copy mut, copy the rest */ big = other.big; return *this; }
  ThreadSafeLazy(ThreadSafeLazy&& other) noexcept { /* do not copy mut, copy the rest */ big = move(other.big); }
  ThreadSafeLazy& operator=(ThreadSafeLazy&& other) noexcept { /* do not copy mut, copy the rest */ big = move(other.big); return *this; }
  void some_method(...) const {
    MakeSureReady();
    big.something(...);
  }

private:
  // should keep big and mut mutable to modify from const fn
  void MakeSureReady() const {
    scoped_lock loc(mut);
    if (!big) {
      big.emplace(...);
    }
  }
};


class ThreadSafeLazyCallOnce : public Lazy
{
  mutable once_flag flag;// not copyable, not movable, need custom copy ctors, assignment etc
public:

  ThreadSafeLazy(const ThreadSafeLazy& other) noexcept { /* do not copy mut, copy the rest */ big = other.big; }
  ThreadSafeLazy& operator=(const ThreadSafeLazy& other) noexcept { /* do not copy mut, copy the rest */ big = other.big; return *this; }
  ThreadSafeLazy(ThreadSafeLazy&& other) noexcept { /* do not copy mut, copy the rest */ big = move(other.big); }
  ThreadSafeLazy& operator=(ThreadSafeLazy&& other) noexcept { /* do not copy mut, copy the rest */ big = move(other.big); return *this; }
  void some_method(...) const {
    MakeSureReady();
    big.something(...);
  }

private:
  // should keep big and flag to modify from const fn
  void MakeSureReady() const {
    if (!big) {
      call_once(flag, [&]() {
        if (!big) { big.emplace(...); }
      });
    }
  }
};
// source: https://www.cppstories.com/2019/11/lazyinit-multithreading/
```

How to deal with copy/move of mutex member of a class?
```cpp
class A
{
  #if CPP11
    using MutexType = std::mutex;
    using ReadLock =  std::unique_lock<MutexType>;
    using WriteLock = std::unique_lock<MutexType>;
  #endif
  #if CPP14
    using MutexType = std::shared_timed_mutex;          // or recursive_mutex for (this == &rhs)
    using ReadLock =  std::shared_lock<MutexType>;
    using WriteLock = std::unique_lock<MutexType>;
  #endif
  mutable MutexType mut_;

  std::string field1_;
  std::string field2_;

private:
  // helper constructor
  A(const A& a, ReadLock rhs_lk) // lock by value
    : field1_(a.field1_), field2_(a.field2_)
  {}

public:
  A(const A& a) : A(a, ReadLock(a.mut_))
  {}

  A(A&& a) {
    // do not need to lock this->mut_ in this ctor,
    // only 1 thread could construct this object
    WriteLock rhs_lk(a.mut_);
    field1_ = std::move(a.field1_);
    field2_ = std::move(a.field2_);
  }

  A& operator=(const A& a) {
    if (&x != &y) {
      WriteLock lhs_lk(x.mut_, defer_lock);
      ReadLock rhs_lk(y.mut_, defer_lock);
      lock(lhs_lk, rhs_lk);
      x.field1_ = y.field1_;
      x.field2_ = y.field2_;
    }
  }

  A& operator=(A&& a) {
    if (&x != &y) {
      WriteLock lhs_lk(x.mut_, defer_lock);
      WriteLock rhs_lk(y.mut_, defer_lock);
      lock(lhs_lk, rhs_lk);
      x.field1_ = move(y.field1_);
      x.field2_ = move(y.field2_);
    }
  }

  friend void swap(A& x, A& y) noexcept
  {
    if (&x != &y) {
      WriteLock lhs_lk(x.mut_, defer_lock);
      WriteLock rhs_lk(y.mut_, defer_lock);
      lock(lhs_lk, rhs_lk);
      using std::swap;
      swap(x.field1_, y.field1_);
      swap(x.field2_, y.field2_);
    }
  }
};

// source: https://stackoverflow.com/questions/29986208/how-should-i-deal-with-mutexes-in-movable-types-in-c/29988626#29988626
```

## Dump predefined macros
```text
echo | g++ -std=c++20 -dM -E -x c++ -
echo | clang -dM -E -x c++ -
```

## Watch memory allocation
```cpp
void* operator new(std::size_t count)
{
  void* ptr = ::malloc(count);
  cout << "  " << count << " bytes (" << ptr << ")" << endl;
  return ptr;
}

void operator delete(void* ptr) noexcept
{
  cout << "  delete(" << ptr << ")" << endl;
  std::free(ptr);
}

/*
void operator delete(void* ptr, std::size_t count) noexcept;   // preferred over delete(void*)

void* operator new[](std::size_t count);
void operator delete[](void* ptr) noexcept;
void operator delete[](void* ptr, std::size_t count) noexcept;   // preferred over delete[](void*)

struct X {
  static void* operator new(std::size_t count);
  static void operator delete(X* ptr) noexcept;
  static void operator delete(X* ptr, std::size_t count) noexcept;

  static void* operator new[](std::size_t count);
  static void operator delete[](X* ptr, std::size_t count) noexcept;
};
*/

vector v(100); // watch this allocate and free memory
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

## Copyable Moveable

```cpp
class Copyable                                              class NotCopyable
{                                                           {
public:                                                     protected:
  Copyable() = default;                                       NotCopyable() = default;
  ~Copyable() = default;                                      ~NotCopyable() = default;
                                                            private:
  Copyable(Copyable& rhs) = default;                          NotCopyable(const NotCopyable& rhs) = delete;
  Copyable& operator=(Copyable& rhs) = default;               NotCopyable& operator=(const NotCopyable& rhs) = delete;
};                                                          };

class Moveable                                              class NotMoveable
{                                                           {
public:                                                     public:
  Moveable() = default;                                       NotMoveable() = default;
  ~Moveable() = default;                                      ~NotMoveable() = default;
                                                            private:
  Moveable(Moveable&& rhs) = default;                         NotMoveable(NotMoveable&& rhs) = delete;
  Moveable(const Moveable&& rhs) = default;                   NotMoveable(const NotMoveable& rhs) = delete;
  Moveable& operator=(Moveable&& rhs) = default;              NotMoveable& operator=(NotMoveable&& rhs) = delete;
  Moveable& operator=(const Moveable& rhs) = default;         NotMoveable& operator=(const NotMoveable& rhs) = delete;
};                                                          };

class MoveNoCopy {                                          class NoMoveNoCopy {
protected:                                                  protected:
  MoveNoCopy() = default;                                     NoMoveNoCopy() = default;
  MoveNoCopy(MoveNoCopy&&) = default;                         NoMoveNoCopy(NoMoveNoCopy&&) = delete;
  MoveNoCopy(const MoveNoCopy&) = delete;                     NoMoveNoCopy(const NoMoveNoCopy&) = delete;
  MoveNoCopy& operator=(MoveNoCopy&&) = default;              NoMoveNoCopy& operator=(NoMoveNoCopy&&) = delete;
  MoveNoCopy& operator=(const MoveNoCopy&) = delete;          NoMoveNoCopy& operator=(const NoMoveNoCopy&) = delete;
};                                                          };
```

## Method chaining

```cpp
class A {
public:
  A& value1(int a) { value1_ = a; return *this; }
  A& name1(const char* s) { name1_ = s; return *this; }

private:
  int value1_ = 0;
  const char* name1_ = nullptr;
};

A a;
a.value1(10).name1("hello");
foo(a);

foo(A().value1(10).name1("hello"));
```

## Copy into a vector
```cpp
#include <algorithm>
#include <iterator>

vector<int> src;
vector<int> dst;

copy(src.begin(), src.end(), back_inserter(dst));
```

### Copying

```cpp
class C {
  vector<int> vi;
  C(vector<int> v) : vi(move(v)) { /* do not use v here, it is moved. use vi */ }
};

/* lvalue */                       | /* rvalue */                       | /* l/r-value */
C(const vector<int>& v) : vi(v) {} | C(vector<int>&& v) : vi(move(v)) {}| C(vector<int> v) : vi(move(v)) {}
```

## CPP Features

### CPP Data Types
```cpp
#include <cstdint>

bool;
char; byte; unsigned char; int8_t; uint8_t;
short; short int; unsigned short; unsigned short int; int16_t; uint16_t;
int; unsigned int; int32_t; uint32_t;
long; long int; unsigned long; unsigned long int;  // 32-bit on LLP64, 64-bit on LP64
long long; long long int; unsigned long long; unsigned long long int; int64_t; uint64_t;

float;        // 4 bytes
double;       // 8 bytes
long double;  // 16 bytes or 8 bytes

void;

enum;     // unscoped enum, can be converted to int implicitly
enum Color { red, green, blue }; Color r = red;
enum Color : byte { red, green, blue };

enum class; enum struct;      // scoped enum, need static_cast to convert to int
enum class Color { red, green, blue }; Color r = Color::red;
union;
class; struct;

```

### CPP Number limits

```cpp
#include <limits>         | #include <limits.h>

int a = INT_MIN, b = INT_MAX;                 // c/c++ limits

int a = std::numeric_limits<int>::min(),      // c++ limits
    b = std::numeric_limits<int>::max();

```

### Function pointers
```cpp
R (*fp)(Arg1, Arg2);
fp = &sum;
v = fp(a, b);

R (A::*memfp)(Arg1, Arg2);
memfp = &A::foo;
A a;
v = (a.*memfp)(x, y);

```

### CPP File IO

#### CPP CSV Files
```cpp
#include <sstream>
#include <iomanip>
#include <ranges>
#include <string>

const char* csv_data = R"(field1,field2,field3
10,40,"hello world"
20,80,"abcd efg"
)";

istringstream ss(csv_data);
string line;
while (getline(ss, line)) {
    for (auto v : rv::split(line, ',')){
        // cout << boost::core::demangle(typeid(v).name()) << endl;
        cout << quoted(string_view(v)) << endl;
    }
    cout << endl;
}

// alternatively
#include <cstdio>  // for constant EOF
#include <fstream>
#include <string>

istringstream ss(csv_data);
string record, line;
while (getline(ss, line)) {
    istringstream line_ss(line);
    while (getline(line_ss, record, ',')) {
        cout << record << endl;
    }
}

// alternatively
#include <cstdio>  // for constant EOF
#include <fstream>
#include <string>

istringstream ss(csv_data);
string record;
while (ss.peek() != EOF) {        // std::char_traits<char>::eof()
    getline(ss, record, ',');
    cout << record << endl;
}
```

#### fstream

```cpp
#include <fstream>
#include <string>

ifstream ifs;
ifs.open(filepath);
if (ifs.fail()) {
    // error
}
string line;
while (ifs.peek() != EOF) {
    getline(ifs, line);
}
```

### Structured binding

```cpp
auto [x, y] = get_point(n);

tuple<int, int> t(100, 200);
const auto& [x, y] = t;

int a[] = { 1, 3 };
auto& [x, y] = a;

struct S { int a; int b };
S s { 1, 10 };
auto [ x, y ] = s;    // accessible data members, in order declared in struct/class

int a = 1, b = 10;
const auto& [x, y] = tie(a, b);  // tie creates a tuple of lvalue references

int p, q;
tie(p, q) = tuple<int, int>(100, 200);

map<int, int> m { {1, 100}, {2, 200}, };
for (auto [x, y] : m)           | for (auto v : m)
{                               | {
  ...                           |   v.first; v.second;
}                               | }
```

Compatible type T, if the following metafunctions are available:
- `std::tuple_size<T>::value` number of T's elements
- `std::tuple_element<I>::type` type of I-th element
- `return_type std::get<I>(T)` retrieves I-th element

Already defined for `std::tuple, pair, array`

For a custom class, example:

```cpp
#include <utility>
#include <type_traits>
class A {
  ...
  // option 1 for get(), as a member
  template<size_t I> tuple_element_t<I, A>& get() &
  {
    if constexpr (I == 0) return int_val;
    if constexpr (I == 1) return char_val;
    ...
  }
  ... also need const, rvalue ref ...
  template<size_t I> tuple_element_t<I, A> const& get() const { ... }
  template<size_t I> tuple_element_t<I, A>& get() && { ... return std::move(int_val); ... }
  template<size_t I> tuple_element_t<I, A> const& get() const&& { ... return std::move(int_val); ... }
  // option 2 for get(), use helper
  template<size_t I, typename T> auto&& get_helper(T&& t)
  {
    static_assert(I < 5, "Index out of bounds for A");
    if constexpr (I == 0) return std::forward<T>(t).int_val;
    if constexpr (I == 1) return std::forward<T>(t).char_val;
    if constexpr (I == 2) return std::forward<T>(t).float_val;
    ...
  }
  template<size_t I> auto&& get() & { return get_helper<I>(*this); }
  template<size_t I> auto&& get() && { return get_helper<I>(*this); }
  template<size_t I> auto&& get() const& { return get_helper<I>(*this); }
  template<size_t I> auto&& get() const&& { return get_helper<I>(*this); }
  // see alternative get() below, as non-member
};

namespace std {
  template<> struct tuple_size<A> { static constexpr size_t value = 5; };
    // alternative
  template<> struct tuple_size<A> : integral_constant<size_t, 5> {};

  template<> struct tuple_element<0, A> { using type = int; };
  template<> struct tuple_element<1, A> { using type = char; };
  template<> struct tuple_element<2, A> { using type = float; };
  template<> struct tuple_element<3, A> { using type = string; };
  template<> struct tuple_element<4, A> { using type = int; };
    // alternative
  template<size_t I> struct tuple_element<I, A>
    : conditional<I == 0, int,
        conditonal<I == 1, char,
          conditional<I == 2, float,
            conditional<I == 3, string, int>
          >
        >
      >
  {
    static_assert(I < 5, "Index out of bounds for A">);
  };
    // alternative
  template<size_t I> struct tuple_element<I, A>
    : tuple_element<I, tuple<int, char, float, string, int>>
  {};

  // alternative get, possible to do this way for an existing class that can't modify
  template<size_t I> tuple_element_t<I, A>& get(A& a)
  {
    if constexpr (I == 0) return a.int_val;
    if constexpr (I == 1) return a.char_val;
    ...
  }

  // alternative get, using helper
  template<size_t I, typename T> auto&& A_get_helper(T&& t)
  {
    static_assert(I < 5, "Index out of bounds for A");
    if constexpr (I == 0) return std::forward<T>(t).int_val;
    if constexpr (I == 1) return std::forward<T>(t).char_val;
    if constexpr (I == 2) return std::forward<T>(t).float_val;
  }
  template<size_t I> auto&& get(A& t) { return A_get_helper<I>(t); }
  template<size_t I> auto&& get(const A& t) { return A_get_helper<I>(t); }
  template<size_t I> auto&& get(A&& t) { return A_get_helper<I>(move(t)); }
  template<size_t I> auto&& get(A const&& t) { return A_get_helper<I>(move(t)); }
}
```

See: [C++ on Sea 2020 - S/B uncovered](https://youtu.be/uZCvz-E1heA?t=1592)

### Swap

3 ways to define swap:

```cpp
// method 1: member swap, std::swap specialization
namespace X {
  class A {
    void swap(A& b) noexcept;               // member swap
  };
}
namespace std {
  template<>                              // full specialization
  void swap(A& a, A& b) noexcept { a.swap(b); }    // calls member swap
}

// method 2: overload std::swap, defined in same scope as class A
namespace X {
  class A {
    void swap(A& b) noexcept;             // member swap
  };

  // same scope as the class
  void swap(A& a, A& b) noexcept { a.swap(b); }    // calls member swap
}

// method 3: define swap() as a friend function
namespace X {
  class A {
    friend void swap(A& a, A& b) noexcept {
      ...
    }
  };
}

// usage:
template<typename T>
void some_func(T& obj)
{
  T tmp;
  using std::swap;
  swap(tmp, obj);   // would try X::swap() before std::swap()
}
```

## Crazy STL

### Smart Pointers

```cpp
shared_ptr<A>       // reference counted raw pointer
weak_ptr<A>         // does not change reference count
unique_ptr<A>       // unique ownership, not copyable

auto uptr = make_unique<A>();
uptr->foo();

auto us = make_unique<A[]>(10);
us[2].foo();

auto sp = make_shared<A>();
shared_ptr<A> sp2 = sp; // ref_count++
assert(sp.use_count() == 2);    // use_count() gives ref_count
sp->foo();

auto wp = weak_ptr(sp);
shared_ptr<A> = wp.lock();  // convert weak into shared
```

### enable if

`enable_if< Condition, SomeType >` -- if `Condition` is true, then `enable_if::type == SomeType`, otherwise it is not defined.

```cpp
template<typename Cond, typename Type>
struct enable_if {};                            // empty

template<typename Type>
struct enable_if<true, Type> {
  using type = Type;                            // defined when Cond = true
};
```

#### Usage - 4 ways
```cpp
// usage:
// #1 - use non-type parameter for template
template<
  typename T,
  enable_if<is_integral<T>::value, Blah>::type = SomeBlahValue    // Cond is true, then this matches
                                                                  // otherwise, that type is not defined
                                                                  // and this template definition does not match
                                                                  // Blah can be int, bool, or anything else, does not matter
>
void func() { .... }

// #2 - use return type of function
template<typename T>
typename enable_if<Cond>::type            // return type, void (default param)
foobar()                                  // i.e. function: void foobar(), only if Cond is true
{}

// #3 - enable via function parameter
template<typename T>
void foobar(
  T t,
  typename enable_if<Cond>::type* = nullptr   // void* = nullptr, if Cond is true, foobar is not defined if Cond is false
)
{}

// #4 - use type parameter for template
template<
  typename T,
  typename = enable_if<Cond>::type          // enabled if Cond is true
>
void foobar(T t)
{}
```


### any, variant, optional

#### Usage - any (type-safe void*)
```cpp
#include <any>
any a = 1;
any b = "hello";
a = b;
a = "world";
any_cast<string>(a)
a.has_value()
a.reset()
a.emplace(ctor args)

vector<any> va = { 1, 20.0, "hello", A(), };
```

#### Implementation idea - any
```cpp
struct any
{
  void* data_;
  std::type_info const& (*getType_)();
  void* (*clone_)(void* otherData);
  void (*destroy_)(void* data);

  template<typename T>
  explicit any(T&& value)
    : data_{new T{std::forward<T>(value)}}
    , getType_{[]() -> std::type_info const&{ return typeid(T); }}
    , clone_([](void* otherData) -> void* { return new T(*static_cast<T*>(otherData)); })
    , destroy_([](void* data_) { delete static_cast<T*>(data_); })
  {
  }

  any(any const& other)
    : data_(other.clone_(other.data_))
    , getType_(other.getType_)
    , clone_(other.clone_)
    , destroy_(other.destroy_)
  {
  }

  ~any()
  {
    destroy_(data_);
  }
};

// https://www.fluentcpp.com/2021/02/05/how-stdany-works/
```

#### Usage - variant (type-safe union)
```cpp
variant< int, float > v;
v = 41;
int i = get<int>(v);
int i = get<0>(v);
get<float>(v); // throws bad_variant_access, stored int above

holds_alternative<int>(v) == true;

visit( [](auto&& val) { cout << val; }, v );

// https://github.com/mpark/variant
// https://github.com/groundswellaudio/swl-variant
```

#### Implementation idea - variant
```cpp
template<typename ...Types>
class Variant
{
  size_t active_idx;
  VariadicUnion<Types...> data;
public:
  template<typename T>
    requires (same_as<T, Types> or ... )
  Variant(T&& v)
    : active_idx( PackIndex<T, Types...>::value )
    , data( integral_constant<size_t, PackIndex<T, Types...>::value>(), forward<T>(v) )
  {}

  // template<typename T> Variant& operator=(T&& v);

  ~Variant() {
    data.destroy(active_idx);
  }

  size_t index() const { return active_idx; }

  template<std::size_t I>
  auto& get()
  {
    assert( I == active_idx );
    return data.template get<I>();
  }
};

// ---------------------------------------------------------------------------
template<typename T1, typename ...Ts>
struct PackIndex;

template<typename T1, typename ...Ts>
struct PackIndex<T1, T1, Ts...>
  : integral_constant<size_t, 0>
{};

template<typename T1, typename U1, typename ...Ts>
struct PackIndex<T1, U1, Ts...>
  : integral_constant<size_t, 1 + PackIndex<T1, Ts...>::value>
{};

// ---------------------------------------------------------------------------
template<typename T1, typename ...Ts>
union VariadicUnion                // recursive definition of union
{
  T1 first;
  VariadicUnion<Ts...> rest;

  template<typename U>
  VariadicUnion( integral_constant<size_t, 0>, U&& u)
    : first( forward<U>(u) )
  {}

  template<size_t I, typename U>
  VariadicUnion( integral_constant<size_t, I>, U&& u)
    : rest( integral_constant<size_t, I-1>(), forward<U>(u) )
  {}

  template<std::size_t I>
  auto& get() {
    if constexpr (I == 0) {
      return first;
    }
    else {
      return rest.template get<I-1>();
    }
  }

  void destroy(std::size_t I)
  {
    if (I == 0) {
      first.~T1();
    }
    else {
      rest.destroy(I-1);
    }
  }
};

template<typename T1>
union VariadicUnion<T1>                       // base case
{
  T1 first;

  template<typename U>
  VariadicUnion( integral_constant<size_t, 0>, U&& u)
    : first( forward<U>(u) )
  {}

  template<std::size_t I>
  auto& get() { return first; }

  void destroy(std::size_t I)
  {
    assert(I == 0);
    first.~T1();
  }
};

// ---------------------------------------------------------------------------
```

#### Usage - optional

contains storage for the object and manages its lifetime

```cpp
#include <optional>

optional<int> o;
optional<int> o(100);
o.has_value() == bool(o)
o.emplace(100);
nullopt == optional<int>{}
int i = *o;
int i = o.value();
int i = o.value_or(10);
*o = 20;
o.reset();

optional<string> o;
o->size();
auto taken = *move(o);

/* has value */                             | /* no value */
optional<A> o;                              |
o = optional<A>{A{}}                        | o = optional<A>{}
o = A{}                                     | o = {}
o = make_optional<A>()                      | o = nullopt
o.emplace()                                 | o.reset()
```

#### Implementation idea - optional
```cpp
struct Optional<T>  // messsy version
{
  bool got_value;
  aligned_storage_t<sizeof(T), alignof(T)> buf;  // space for T contained_value
  optional(const T& t) : got_value(true) { ::new ((void*)&buf) T(t); } // in-place new
  ~optional() { if (got_value) { reinterpret_cast<T&>(buf).~T(); } }   // destructor
};

struct Optional<T>  // better, with anonymous union
{
  union {
    char dummy;
    T val;
  };
  bool engaged;
  optional() : dummy(0), engaged(false) {}
  optional(const T& t) : val(t), engaged(true) {}
  ~optional() {
    if constexpr (!is_trivially_destructible<T>{}) {
      if (engaged) val.~T();
    }
  }
};

// see: https://www.club.cc.cmu.edu/~ajo/disseminate/2017-02-15-Optional-From-Scratch.pdf
// https://www.club.cc.cmu.edu/~ajo/
```

### Tag Dispatch

Use a type to overload an implementation

```cpp
struct RandomIteratorTag {};
struct ForwardIteratorTag {};

void advance_impl(Iter& iter, int skip, RandomIteratorTag)
{
  iter += skip;
}

void advance_impl(Iter& iter, int skip, ForwardIteratorTag)
{
  while (skip > 0) {
    iter++;
    --skip;
  }
  return iter;
}

void advance(Iter& iter, int dist)
{
  advance_impl(iter, dist, Iter::category)
}
```

### Type Erasure

```mermaid
---
title: Type Erasure
---
classDiagram

class Object {
  Ctor~T~(T)
  foo()
  obj : Concept
}

class Concept {
  <<interface>>
  foo()
}

class Model~T~ {
  inst : T
  foo()
}

class T {
  foo()
}

note for Model "delegates to T.foo()"

Concept <|-- Model
Object o-- Concept : obj
Model~T~ --> T : inst

note "Object.foo -> Concept.foo -> Model<T>.foo -> T.foo()\no1 = Object(MyClass1());\no1.foo();\no2 = Object(MyClass2());\no2.foo()"

class MyClass1 {
  foo()
}

class MyClass2 {
  foo()
}
```

Example:
```cpp
class Wrapper {
  Concept* concept;

  class Concept {
  public:
    virtual void foobar() = 0;
  };

  template<typename T>
  class Model : public Concept {
    T instance;
  public:
    Model(T& o) : instance(o) {}

    void foobar() override final {
      instance.foobar();
    }
  };

public:
  template<typename T>
  Wrapper(T&& o) : concept(new Model<T>(o)) {}
  ~Wrapper() { delete concept; }

  void foobar() {
    concept->foobar();
  }
};

class MyImpl1 {
public:
  void foobar() {
    cout << "Impl 1" << endl;
  }
};

class MyImpl2 {
public:
  void foobar() {
    cout << "Impl 1" << endl;
  }
};

vector<Wrapper> v;
v.push_back(MyImpl1());
v.push_back(MyImpl2());

for (auto& x : v) {
  x.foobar();         // will call MyImpl1/MyImpl2 foobar()
}
```

### CRTP

```mermaid
---
title: CRTP
---

classDiagram
class Base["Base< Derived >"] {
  + someBigCommonFunction()
}

class Base1~Derived1~ {
  + someBigCommonFunction()
}

class Base2~Derived2~ {
  + someBigCommonFunction()
}

note "calls Derived->customFooBar()"

class Derived1 {
  + customFooBar()
}

class Derived2 {
  + customFooBar()
}
Base1 <|-- Derived1
Base2 <|-- Derived2
```

```cpp
template<typename Derived>
class Base
{
  // calls foobar() which is customized in derived classes
  void someBigCommonFunctionWith1Difference()
  {
    ...
    static_cast<Derived*>(this)->foobar();
    ...
  }
};

class Derived1 : public Base<Derived1>
{
public:
  void foobar()
  {
    cout << "Custom definition of Derived1.foobar\n";
  }
};

class Derived2 : public Base<Derived2>
{
public:
  void foobar()
  {
    cout << "Custom definition of Derived2.foobar\n";
  }
};

Derived1 d1;
Derived2 d2;
d1.someBigCommonFunctionWith1Difference();
d2.someBigCommonFunctionWith1Difference();
```

### Return type resolver
```cpp
class MakeContainer
{
    int size;
  public:
    explicit MakeContainer(int size) : size(size) {}

    template<typename Container>
    operator Container()                  // conversion operator
    {
      Container c(size);

      return c;
    }
};

// deduce which conversion operator to call from type of variable used for return value
vector<int> vi = MakeContainer(9);    // will create vector of int
list<A> va = MakeContainer(2);        // will create list of A

// does not even have to use templates for conversion operator

class FromString
{
  const string& source;
public:
  explicit FromString(const string& src) : source(src) {}

  operator int() { return stoi(source); }
  operator double() { return stod(source); }
};

int ival = FromString("1122");          // implicit: FromString(...).operator int()
double dval = FromString("0.5");
```

### virtual constructor idiom

```cpp
struct IAnimal abstract
{
  virtual IAnimal* createNew() = 0;
  virtual IAnimal* copy() = 0;
};

template<typename Concrete>
struct AnimalBase : public IAnimal
{
  IAnimal* createNew() override final
  {
    return new Concreate();
  }

  IAnimal* copy() override final
  {
    return new Concrete(*static_cast<const Concrete*>(this));
  }
};

struct Dog : public AnimalBase<Dog> {};
struct Cat : public AnimalBase<Cat> {};

void foo()
{
  IAnimal* animal = new Dog();

  IAnimal* new_dog = animal->createNew();
  IAnimal* dog_copy = animal->copy();
}
```

### std string_view

should not outlive the pointed-to char array. this is a non-owning reference to a string.

```cpp
#include <string_view>

using namespace std::literals;

string_view s1 = "abcd"sv;        // literal string_view
string s2 = "abcd"s;              // literal string

string_view sv = str;
string_view sv(data, len);
string_view sv(c_str);
string_view sv2 = sv.substr(m, n);

sv.find_first_not_of(' ');

cout << sv << endl;

string_view sv(s.begin(), s.end()); // s is a std::string
```

### std span

span is a generalized string_view, can be used for other range types, not just strings. for view of a contiguous sequence of data.

```cpp
int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, };
vector<int> vec = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, };
span<int, 10> arr_span { arr };     // static length
span<int>     dyn_arr_span { arr }; // dynamic length
span<int>     vec_span { vec };

span<int> sp = arr_span.subspan(3, 5);
arr_span.first(4);  // sub-span of first 4 items
arr_span.last(2);   // sub-span of last 2 items

span<char> sp { s };
span<char> sp { s, 5 };   // count=5

span<int> sp { begin(vec), end(vec) };
span<int> sp { begin(vec), 3 };   // count=3
```


### std function

`std::function` is a polymorphic callable wrapper, is implemented using type-erasure idiom.

```cpp
#include <iostream>
#include <functional>

using namespace std;
using namespace std::placeholders;

inline double add(double a, double b) { return a+b; }

struct Sub {
  double operator()(double a, double b) { return a-b; }
};

inline double multThree(double a, double b, double c) {
  return a*b*c;
}

Sub sub;

auto mult = std::bind(multThree, _1, _2, 1.0);

auto div = [](double a, double b) { return a/b; };

std::function<double(double,double)> arr[] = {
  add,        // function
  sub,        // function object
  mult,       // function object created by bind
  div,        // lambda expression
};

for (auto& f : arr) {
  cout << f(5.0, 2.5) << endl;
}
```

### lambda expanded
```cpp
int x, y;
auto f = [&x, y](double a, double b) { return (a+b+x+y); };

// equivalent to:
class Lambda  // closure type
{
  // closure
  int &x;
  int y;
public:
  Lambda(int& x, int& y) : x(x), y(y) {}

  // callable, note this will become a template function lambda uses auto for params
  double operator()(double a, double b) const              // const callable, unless mutable lambda
  { return a+b+x+y; }

  // oh i get it now, this is so that it can be implicitly
  // not really necessary, this is getting generated when I assign lambda to a std::function
  using retType = double (*)(double, double);
  constexpr operator retType() const noexcept { return invoke; }
  static double invoke(double a, double b) {
    Lambda l{};
    return l.operator()(a, b);
  }
};

Lambda f{x, y}; // closure x, y

f.operator()(1.9, 2.3);    // callable
```

### Using lambdas
```cpp
auto sumInt = [](int a, int b) { return a+b; };             // ordinary

auto addAnything = [](auto a, auto b) { return a+b; };      // can pass any type data for a, b

auto sumDec = [](auto a, decltype(a) b) { return a+b; };    // not any b, convertible to type of 'a'

auto sumTmpl = []<typename T>(T a, T b) { return a+b; };    // templatized
```

More examples:
```cpp
[](const Person& a, const Person& b) { return a.name < b.name; }
    // immutable closure, it is a const function
    // return type - deduced - bool, can instead give trailing return type
    // not noexcept by default, if needed, can declare with noexcept

[](const Person& a, const Person& b) -> bool { return a.name < b.name; }
[](const Person& a, const Person& b) mutable { return a.name < b.name; }
[](const Person& a, const Person& b) noexcept { return a.name < b.name; }

[](int i) { return i*i; }
    // lambda expressions with empty closure can be used as function pointers
    // void foo(int (*)(int) f); foo([](int i) {return i*i; });
auto* fptr = +[](int i) { return i*i; };          // idiom: unary plus operator trick
{ int i, j = 0; auto f = [=] { return i==j; }}    // capture by value, =
    // only capture local variables, can not capture global/static variables
{ int i, j = 0; auto f = [&] { return i==j; }}    // capture by reference, &

struct X {
  int i_;
  void foo() {
    auto f = [this] {                             // capture this, to use members i_
      cout << i_;                                 // __this->i_
    };
    ...
  }
};

int foo() {
  static int k = 42;
  int m = 100;
  auto f = [=] { ++k; --m; };                     // not going to capture 'k' by value, 'm' is by val
  f();                                            // will modify that outer k, local m is not changed
  return k;                                       // will return 43
}

// idiom: immediately invoked function expression (IIFE)
[] {...} ();                                      // call it immediately, temporary lambda
const Foo foo = [] {
  if (hasDatabase) { return getFooFromDatabase(); }
  else { return getFooFromElsewhere(); }
} ();                                             // trick to conditional initialization

v.emplace_back([] {...}());                       // similar idea, passing return value of lambda
v.emplace_back(invoke([] { ...}));                // explicitly invoke the lambda, less confusing

// idiom: call-once lambda (daisy hollman, what you can learn from being too cute)
struct X {
  X() {
    static auto _ = [] { ... } ();                // we want it to be called only once
  }
};
X x1, x2, x3;                                     // called only once

// generic lambdas
[](auto i) { ... i ... };                         // template<T> call_operator(T i) const {...}

// perfect forwarding, auto ref ref
[&v](auto&& x) {                                  // template<T> call_oper(T&& x) const { __v.push_back(...); }
  v.push_back(forward<decltype(x)>(x));
};

// variadic templates
[](auto&&.. args) {
  (cout << ... << args);                          // fold expression
} (123, "hello", 'a', 4.0);

// idiom: variable template lambda (bjorn fahller)
template<typename T>                              // not just the callable, the lambda closure type also is a template
constexpr auto x = [](auto y) {
  return (T)y;                                    // cast to type T
}

// example:
template<typename T> constexpr auto duration_cast = [](auto d) {
  return std::chrono::duration_cast<T>(d);
}
using ns = std::chrono::nanoseconds;
using ms = std::chrono::milliseconds;
using us = std::chrono::microseconds;
struct Time {
  variant<ms, ns> time;
  auto convert(const auto& converter) {
    return visit(converter, time);
  }
};
void foobar() {
  Time t(ns(3000));
  auto in_usecs = t.convert(duration_cast<us>).count();
}

// init capture
unique_ptr<A> ptr;
auto lambda_f_instance = [ptr = std::move(ptr)] { ... ptr.get() ... }
// equiv to
struct LambdaClosureType {
  LambdaClosureType(unique_ptr<A> p) : __ptr(move(p)) {}
  unique_ptr<A> __ptr;
  ... callable ...
} lambda_f_instance {move(ptr)};

// idiom: init capture initialization (bartlomiej filipek - C++ lambda story book)
const string prefix="foo"; // looking for "foobar" in a vector
auto iter = find_if(vs.begin(), vs.end(), [str=prefix+"bar"](const string& s) { return s == str}; );
// versus less efficient version, calculates prefix+"bar" for every item in vs
auto iter = find_if(vs.begin(), vs.end(), [&prefix](const string& s) { return s == prefix+"bar"}; );

// lambdas can be constexpr or consteval, that can execute at compile time
auto f = []() constexpr { return sizeof(void*); };    // compile time
array<int, f()> arr = {};
auto g = [](int i) consteval { return i*i; };         // compile time only
array<int, g(5)> arr = {};                            // ok
g(x); // error, not a constant

// idiom: lambda overload set (uses CTAD)
// idea -- lambda's are conceptually classes, and you should be able to inherit from them
template<typename... Ts>                      // variadic args will be lambdas
struct overload : Ts... {                     // we inherit from those lambdas
  using Ts::operator()...;                    // we pull in the callable operator from all of them
};

overload f = {                                // note: CTAD use, haven't given template arg types
  [](int i) { cout << "Wonderful, called with int"; },
  [](float f) { cout << "Call with float detected"; }
};
f(10);  // Wonderful, called with int
f(2.5); // Call with float detected
variant<int, float> v = 3.9;
visit(f, v);        // Call with float detected

// structured binding captured in lambdas
auto [x, y] = Point();
auto f = [=] {
  cout << x << ", " << y << endl;
};
// variadic args captured in lambdas
auto foo(auto... args) { cout << sizeof...(args) << endl; }
template<typename... Args>
auto delay_invoke_foo(Args... args) {
  return [args...]() -> decltype(auto) {
    return foo(args...);
  }
}

erase_if(v.begin(), v.end(), [](auto i) { ... i ... });           // callable is a template, but no name for the type
erase_if(v.begin(). v.end(), []<typename T>(T i) { ... i ...});   // can give the template type a name, can specify constraints etc. (C++20)

// lambda as a data member of a class
class W {
  auto mem_f_ = []{};    // error: data member with auto not allowed
  decltype([]{}) mem_f_; // ok in C++20
};
// benefit: now can define template parameters that are lambdas
// note: earlier we could not do this in template definition at compile time,
// had to pass it as constructor param, which is for later (run time)
typename<typename T>
using UniquePtrTypeWithMyOwnDeleter = unique_ptr<T, decltype<[](T* t) { myDeleter(t); }>>;
UniquePtrTypeWithMyOwnDeleter<A> ptr;
// comparison function is a lambda given in template definition at compile time
using WidgetSet = std::set< Widget, decltype([](Widget& a, Widget& b) { return a.x < b.x; })>;
WidgetSet ws;

// compiler generates a different type for every lambda it sees
auto f1 = []{};
auto f2 = []{};     // f1 and f2 have different types, even though lambdas look identical
auto f3 = f1;       // f1, f3 have same type
decltype(f1) f4;    // f1 and f4 have same type
using t = decltype([]{});
t f5, f6;           // f5 and f6 have same type
template<auto = []{}> struct X{};
X x1, x2;           // x1 and x2 have different type, each instantiation is different type
static_assert(typeid(decltype(x1)) == typeid(decltype(x2)), "types are different");
// idiom: unique type generator (kris jusiak)

// idiom (C++23): recursive lambdas
// factorial using lambdas,
// idea 1:
// auto fact = [](int i) { if (i==0); return 1; return i*fact(i-1); };
// cannot refer to fact in its own initializer

// idea 2: use capture by reference, after making lambda a std::function
// ok, but there is an overhead here, function uses type erasure etc.
function<int(int)> fact = [&](int i) { if (i==0) return 1; return i*fact(i-1); };

// idea 3: c++23, "deduce this"
auto fact = [](this aut&& self, int i) { if (i==0); return 1; return i*self(i-1); };

// idiom (C++23): recursive lambda overload set -- ben deane -- deducing this patterns
// binary tree implemented as a variant, use overload defined above
struct Leaf {};
struct Node;
using Tree = std::variant<Leaf, Node*>;
struct Node { Tree left, right; }

int countLeaves(const Tree& tree) {
  return visit(
    overload {
      [] (const Leaf&) { return 1; },
      [] (this const auto& self, const Node* node) -> int {
        // self is the compiler generated type for "overload" template instantiated
        return visit(self, node->left) + visit(self, node->right);
      }
    },
    tree
  );
}
```

### Class Template Argument Deduction (CTAD)
```cpp
vector vi = { 1, 2, 3, 4}; // vector<int> deduced from the initializer list with integers
```

### std bind
```cpp
#include <functional>

using namespace std::placeholders;

double divide(double a, double b) { return a/b; }

auto calcOneByTwo = bind(divide, 1.0, 2.0);       // we get a callable object
double half = calcOneByTwo();                     // call that callable

auto inverse = bind(divide, 1.0, _1);             // 1st param is bound, 2nd is free, placeholder
double half = inverse(2.0);

auto twice = bind(divide, _1, 0.5);              // 2nd arg is bound
double ten = twice(5.0);

```

### sort

```cpp
sort(v.begin(), v.end(), [](const A& a, const A& b) { return a.m1 < b.m1; }); // lambda expr
//  lambda => "closure type" with public inline call operator

sort(v.rbegin(), v.rend()); // reverse order sort
```

### sum of vector

```cpp
#include <algorithm>
int sum = accumulate(v.begin(), v.end(), 0);

#include <numeric>
int sum = reduce(v.begin(), v.end(), 0);
```

### std ranges
```cpp
#include <ranges>
#include <algorithm>

namespace rs = std::ranges;
namespace rv = std::ranges::views;   // same as std::views

using namespace std;

auto print_elem = [](auto const e) {std::cout << e << '\n'; };
auto even = [](auto const i) { return i%2 == 0; };
auto  odd = [](auto const i) { return i%2 != 0; };
auto square = [](auto const i) { return i*i; };

std::string to_roman(int value)
{
   std::vector<std::pair<int, char const*>> roman
   {
      { 1000, "M" },{ 900, "CM" },
      { 500, "D" },{ 400, "CD" },
      { 100, "C" },{ 90, "XC" },
      { 50, "L" },{ 40, "XL" },
      { 10, "X" },{ 9, "IX" },
      { 5, "V" },{ 4, "IV" },
      { 1, "I" }
   };
   std::string result;
   for (auto const & [d, r]: roman)
   {
      while (value >= d)
      {
         result += r;
         value -= d;
      }
   }
   return result;
}

// print vector elements
rs::for_each(crbegin(vi), crend(vi), print_elem);                   | for_each(cbegin(vi), cend(vi), print_elem);
rs::for_each(as_const(vi), print_elem);                             | for (const auto i : vi) { print_elem(i); }

// print vector elements in reverse
rs::for_each(rv::reverse(vi), print_elem);                          | for_each(crbegin(vi), crend(vi), print_elem);
rs::for_each(vi|rv::reverse, print_elem);                           |

// print only even items
rs::for_each(vi|rv::filter(even), print_elem);                      | for_each(cbegin(vi), cend(vi), [](auto i) { if (even(i)) print_elem(i); });


// skip 2 items, print only even from next 5 items
rs::for_each(vi|rv::drop(2)|rv::take(5)|rv::filter(even), print_elem);

// print all from 101 to 200
rs::foreach(rs::iota_view(101, 201), print_elem)                    | for (int n = 101; n < 201; ++n) { print_elem(n); }

// print all roman numerals from 101 - 200
rs::for_each(rv::iota(101, 201), print_elem, /* proj= */ to_roman); | for (int i = 101; i < 201; ++i) { print_elem(to_roman(i)); }

// print roman numerals of last 3 numbers divisible by 7 in the range 101-200
rs::for_each(                                                       | for (int i = 200, count = 0; i > 100 && count < 3; --i) {
    rv::iota(101, 201) |                                            |   if (i % 7 == 0) {
    rv::reverse |                                                   |     print_elem(to_roman(i)); ++count;
    rv::filter([](auto i) { return i%7==0; }) |                     |   }
    rv::take(3) |                                                   | }
    rv::transform(to_roman)                                         |
  ,                                                                 |
  print_elem                                                        |
);                                                                  |

// get a vector of above roman numerals
template <std::ranges::range R>                                     |
auto to_vector(R&& r) {                                             |
    auto r_common = r | std::views::common;                         |
    return std::vector(r_common.begin(), r_common.end());           |
}                                                                   |
                                                                    |
auto vr =                                                           | vector<string> vs;
    rv::iota(101, 201) |                                            | for (int i = 200, count = 0; i > 100 && count < 3; --i) {
    rv::reverse |                                                   |   if (i % 7 == 0) {
    rv::filter([](auto i) { return i%7==0; }) |                     |     vs.push_back(to_roman(i));
    rv::take(3) |                                                   |     ++count;
    rv::transform(to_roman);                                        |   }
vector<string> vs = to_vector(vr);                                  | }
// in C++23, we can use | rs::to<vector<string>>()

// get unique items in reverse sorted order
vector<int> vi;                                                     | sort(vi.begin(), vi.end());
vi = move(vi) | rs::sort | rs::unique | rs::reverse;                | vi.erase(unique(vi.begin(), vi.end()), vi.end());
                                                                    | reverse(vi.begin(), vi.end());

// remove smallest 2 and largest 2 items, the rest in sorted order
vector<int> vi;                                                     | vector<int> vi, vi2; vi2 = vi; sort(v2.begin(), v2.end());
auto vi2 = vi | rs::copy | rs::sort | rs::slice(2, rs::end-2);      | auto first = vi2.begin() + 2, last = vi2.end()-2;
                                                                    | vi2.erase(last, vi2.end());  // not using std::erase()+std::remove(), i.e. erase-remove idiom
                                                                    | vi2.erase(vi2.begin(), first);

// join strings
vector<string> vs { .... };                                         | string joined;
string joined = vs | rs::move | rs::join;                           | for (const auto& w : vs)
string joined = vs | rs::move | rs::join_with(' ');                 | { joined += w; }

// count words separated by space
auto count = rs::distance( rv::c_str(str) | rv::split(' ') );       | istringstream iss(str);
                                                                    | vector<string> words (istream_iterator<string>(iss), istream_iterator<string>());
                                                                    | string token;
                                                                    | int count = 0;
                                                                    | istringstream iss(str);
                                                                    | while (getline(iss, token, ' ') { ++count; }

// sort vector
rs::sort(vi);       // default: rs::less(), increasing order
rs::sort(vi, rs::greater());
rs::sort(rv::reverse(vi));

// composition
auto const vi = rs::iota_view { 1,  21 };   // view factory
for (int i : vi | rv::filter(even) | rv::transform(square)) {...}

// pipe ==> composing views
vi | rv::filter(even) | rv::transform(square);
// same as
rv::transform(
  rv::filter(
    vi
  )
);
```

### Utilities - move forward
```cpp
std::move(v) = static_cast<remove_reference<T>::type&&>(v)
T v;
std::move(v) = static_cast<T&&>(v)

std::forward<T>(arg) = static_cast<T&&>(arg)

remove_reference<T>::type = T
remove_reference<T&>::type = T
remove_reference<T&&>::type = T
```



## Templates

- ellipsis opertor
  - `... T` -- a **parameter pack** of 0+ arguments, example: `template<typename ...T>`, `func( ...v)` is a parameter pack
  - `pattern_with_v ...` -- an **expansion** of parameter pack into separate arguments, whole expression to the left of ellipsis is repeated for all the unpacked arguments, separated with a comma or a space
  - `p1 BINARY_OP ... BINARY_OP p2` -- a **fold** expression of parameter pack. example: `u + ... + v`, or `v + ...`, or `... + v`
- `sizeof...(T)` -- number of arguments in the pack

See also: cpp insights

### Variadic Template Function

```cpp
template<typename ...T> auto sum(const T& ... x) { // zero or more arguments
  return (x + ...);   // fold expression
}
// alternative, recursion
template<typename T1> auto sum(const T1& x1) { return x1; }                     // overload 1
template<typename T1, typename ...T> auto sum(const T1& x1, const T& ... x) {   // overload 2
  return x1 + sum(x ...);
}
```

### Variadic Template Class

```cpp
template<typename ...T> class Tuple
```

### Abbreviated function template, placeholder types
```cpp
void f1(auto v);                          |  template<typename T> void f1(T v);

template<typename T, typename U>          |  template<typename T, typename U, typename W>
void g(T x, U y, auto w);                 |  void g(T x, U y, W w);
```

### template auto
```cpp
template<auto val>                        |  template<typename T, T val>
constexpr auto constant = val;            |  constexpr T constant = val;

// example:
int age = constant<50>;                   |  int age = constant<int, 50>;
```

## Concepts

A _named set of requirements_ is `Concept`

### Very simple example
```cpp
template<typename T>
concept ConceptName = requires(T a)
{
  // satisfied by any type 'T' such that for values 'a' of type 'T', the expression in {...} compiles
  // and its result satisfies constraint_on_result
  { ... } -> constraint_on_result
}

// how to use the concept defined above
template<ConceptName T>
void f(T x) { ... }

SomeTypeThatSatisfiesConceptName y;
f(y);
```

## Print type name
```cpp
// best option
#include <boost/type_index.hpp>
boost::typeindex::type_id_with_cvr<decltype(x)>().pretty_name()

// other options
#include <typeinfo>
typeid(expr).name() // | c++filt -t

#include <boost/core/demangle.hpp>
boost::core::demangle( typeid(expr).name() )

__FUNCSIG__ // MSVC
__PRETTY_FUNCTION__

type_name<T>()

// typeid(expr) -> type_info
#include <cxxabi.h>
int status;
char* name = typeid(expr).name();
char* realname = abi::__cxa_demangle(name, nullptr, nullptr, &status);
free(realname);

// boost type_name
#include <boost/compute/type_traits/type_name.hpp>

boost::compute::type_traits::type_name(expr);
```

### have compiler spit out the type name
```cpp
template<typename T> class TypeDisplayer; // no definition, just declaration

SomeComplexType expr;                       // example: const int v = 10; auto expr = &v;

TypeDisplayer<decltype(expr)> xType;        // compiler will spit an error
// error: ... TypeDisplayer<SomeComplexType> xType has incomplete type ...
```

### utility function for printing type name
```cpp
// usage: cout << type_name<T>() << endl;
template<T>
string type_name()
{
  using TR = std::remove_reference<T>::type;
  string name = boost::core::demangle( typeid(TR).name() );

  if (std::is_const<TR>::value)             name += " const";
  if (std::is_volatile<TR>::value)          name += " volatile";
  if (std::is_lvalue_reference<T>::value)   name += " &";
  if (std::is_rvalue_reference<T>::value)   name += " &&";

  return name;
}

example: type_name<int>()
// see: https://github.com/willwray/type_name
```

## RAII for malloc/free
```cpp
unique_ptr<T, void(*)(void*)> raii_ptr( static_cast<T*>(::malloc(size)), ::free );
```

## Print a vector
```cpp
#include <algorithm>
#include <iterator>

const char* separator;
vector<int> src;
copy(src.begin(), src.end(), ostream_iterator<int>(cout, separator));

auto print_elem = [](const auto& i) { cout << i << ", "; };
for_each(cbegin(src), cend(src), print_elem);
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
  lock_guard guard(mut);            |  call pthread_mutex_lock(mut) # automatic memory barriers
                                    |    if failed call __throw_system_error(...)
  ... critical section ...          |  ...
                                    |  call pthread_mutex_unlock(mut)
}
```

*Guarded* access to *shared* data is slow ... *unguarded* access to *non-shared* data is fast

See also: `std::lock`, takes care of not getting into a deadlock when locking multiple mutexes.

#### Read-Write lock

```cpp
#include <shared_mutex>
shared_mutex mut;  // provides lock/unlock(), lock_shared/unlock_shared()
{
  unique_lock g(mut);   // writer lock
  ... critical ...
}
{
  shared_lock g(mut);   // reader lock
  ... critical ...
}
```

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

#### Atomic for 2 numbers, pack them in 64-bit atomic word

```cpp
struct Pair {
  int32_t a;
  int32_t b;

  // return true if equal, otherwise store update stored values from atomic n
  bool equal(atomic<Pair>& n) {
    if (a == b) return true;
    *this = n.load(memory_order_relaxed);
    return false;
  }
};

atomic<Pair> nums;
```

### Spinlock (not optimized, not good performance)
```cpp
class Spinlock {
public:
  // default constructible
  // noncopyable
  void lock() {
    // not CAS, always exchange, exit loop when 0 -> 1
    while (flag_.exchange(1, memory_order_acquire)) {}
  }
  void unlock() {
    flag_.store(0, memory_order_release);
  }
private:
  atomic<unsigned int> flag_; // 0: unlocked, 1: locked
};
```

#### A bit better, but still not great
```cpp
  void lock() {
      // do not keep updating when it is already 1, avoid locking cache line
    while (
      flag_.load(memory_order_relaxed) ||      // somebody else can slip in before us, its ok
      flag_.exchange(1, memory_order_acquire)
    )
    {}
  }
```

Problem: This is checking very aggressively for the lock. The thread holding the lock doesn't get scheduled to unlock. Solution: yield after trying to lock a few times

#### Optimized spin-lock

```cpp
struct SpinLock {
  SpinLock() = default; // copy constructible
  SpinLock(const SpinLock&) = delete;
  SpinLock& operator=(const SpinLock&) = delete;
  void lock() {
      // yield the cpu every now and then, by sleeping
    for (int i = 0;
      flag_.load(memory_order_relaxed) ||      // somebody else can slip in before us, its ok
        flag_.exchange(1, memory_order_acquire);
      ++i
      ) {
        if (i == 8) {       // 8 or 16 works best
          lock_sleep();
          i = 0;
        }
    }
  }

  void unlock() {
    flag_.store(0, memory_order_release);
  }

private:
  void lock_sleep() {
    static const timespec one_ns = {0, 1};
    nanosleep(one_ns, nullptr);
  }
  atomic<uint> flag_ { 0 };
};
```

#### Read Write Spinlock

```cpp
static constexpr timespec ns = { 0, 1 };
inline void nanosleep(int& i) {
  if (++i == 8) {
    i = 0;
    nanosleep(&ns, NULL);
  }
}

struct RWSpinLock {
  RWSpinLock() = default; // copy constructible
  RWSpinLock(const RWSpinLock&) = delete;
  RWSpinLock& operator=(const RWSpinLock&) = delete;

  void lock() {
    while (true) {
      if (flag_.fetch_sub(unlocked, std::memory_order_acquire) == unlocked) return;
      flag_.fetch_add(unlocked, std::memory_order_relaxed);    // Undo the lock
      for (int i = 0; flag_.load(std::memory_order_relaxed) != idle; ) {
        nanosleep(i);
      }
    }
  }

  void unlock() {
    flag_.store(unlocked, memory_order_release);
  }

  void lock_shared() {
    while (true) {
      if (flag_.fetch_sub(1, memory_order_acquire) > 0) return;
      flag_.fetch_add(1, memory_order_relaxed); // undo subtract
      for (int i = 0; flag_.load(memory_order_relaxed) <= 0; ) {
        nanosleep(i);
      }
    }
  }

  void unlock_shared() {
    flag_.fetch_add(1, memory_order_release);
  }

  bool is_unlocked() const { return flag.load(memory_order_acquire) == unlocked; }
  bool is_locked() const { return flag.load(memory_order_acquire) != unlocked; }
  bool is_rdlocked() const { return (flag.load(memory_order_acquire) & (unlocked-1)) != 0; }
  bool is_wrlocked() const { return (flag.load(memory_order_acquire) == 0; }

private:
  static constexpr long unlocked = 0x1L<<60;            // 0x 1000 0000 0000 0000
  static constexpr long write_lock = 0;                 // 0x 0000 0000 0000 0000
  static constexpr long read_lock_mask = (unlocked-1);  // 0x 7fff ffff ffff ffff ... 1

  atomic<long> flag_ { unlocked };
};
```

### Spinlock to control access to an object

```cpp
template<typename T>
class PtrSpinlock {
public:
  explicit PtrSpinlock(T* p) : p_(p) {}
  T* lock() {
    static const timespec one_ns { 0, 1 };
    T* tmp = nullptr;
    for (
      int i = 0;
      !p_.load(memory_order_relaxed) ||   // cheaper, if p_ != nullptr then try exchange
        !(tmp = p_.exchange(nullptr, memory_order_acquire);
      ++i
    ) {
      if (i == 8) {
        nanosleep(&ns, nullptr);
        i = 0;
      }
    }
    p_save_ = tmp;
    return tmp;
  }

  void unlock() { p_.store(saved_p_, memory_order_release); }
private:
  atomic<T*> p_;
  T* saved_p_ = nullptr;
};

PtrSpinlock<unsigned long> obj { new unsigned long(5) };

void t1() {
  unsigned long* p = obj.lock();
  // have exclusive access to the object
  (*p) = (*p) * 10;
  obj.unlock();
}
```

### Atomic counter, array next empty slot index

Array next empty slot index has a data dependency, we want to ensure that the producer has filled the empty slot, and only then the index is incremented. That is guaranteed with atomic index.

Counter on the other hand is not protecting any other data, so its atomic can be made memory order relaxed. Relaxed are faster on ARM CPUs, but no benefit for x86 CPUs, we any way get the stricter behavior there.

```cpp
class AtomicIndex {                                     |   class AtomicCount {
public:                                                 |   public:
  atomic<uint> N;                                       |     atomic<uint> N;
  uint incr() noexcept                                  |     uint incr() noexcept
    { return 1+N.fetch_add(1, memory_order_release); }  |       { return 1+N.fetch_add(1, memory_order_relaxed); }
  uint get() const noexcept                             |     uint get() const noexcept
    { return N.load(1, memory_order_acquire); }         |       { return N.load(1, memory_order_relaxed); }
};                                                      |   };
                                                        |
AtomicIndex idx;                                        |   AtomicCount count;
idx.incr();                                             |   count.incr();
```

### Thread Safe Unique Pointer

Efficient, but useful only when single producer. No checks at cleanup, cleanup should be handled in some other way.
Can use thread safe shared-ptr if cleanup is that big a deal.

```cpp
template<typename T>
class ThrSafeUniquePtr {
public:
  ThrSafeUniquePtr() = default;
  explicit ThrSafeUniquePtr(T* p) : p_ { p } {}
  ~ThrSafeUniquePtr() {
    del p_.load(memory_order_relaxed);
  }
  // not copyable
  ThrSafeUniquePtr(const ThrSafeUniquePtr& rhs) = delete;
  ThrSafeUniquePtr& operator=(const ThrSafeUniquePtr& rhs) = delete;

  void publish(T* p) noexcept {
    p_.store(p, memory_order_release);
  }
  T* get() const noexcept {
    return p_.load(memory_order_acquire);
  }
private:
  atomic<T*> p_;
};

ThrSafeUniquePtr<MyObj> safe_ptr;

void t1()                                   |   void t2()
{                                           |   {
  safe_ptr.publish(new MyObj());            |     MyObj* p = safe_ptr.get(); if (p != nullptr) { ... }
}                                           |   }
```

Consumer would call `get()`, good to use if returns non-null value. Otherwise publisher not ready with data yet. Should wait for `publish()`.

### Thread Safe Shared Pointer

```cpp
atomic<shared_ptr<T>>
```

### Producer-Consumer

#### SPSC queue using atomic size (lock-free, wait-free)
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

### Memory order

| Memory Order | Description |
|---|---|
| Relaxed `relaxed` | least restricted, only atomic operation guarantee, nothing about visibility of other r/w |
| Acquire-Release `acq_rel` | atomic operation become visible in correct order in all threads |
| Acquire `acquire` | all operations done after the atomic operation should become visible after that operation, should not jump before the atomic operation in any thread |
| Release `release` | all operations done before the atomic operation should become visible before that operation becomes visible to other threads. no guarantee about operations after that atomic operation |

- Note: On X86 processors, all stores are accompanied by a release barrier. So relaxed is not any cheaper on X86.
- Note: Compilers don't optimize by reordering instructions around atomic
- Note: Still may specify memory order explicitly for documenting intent, or for portability to ARM

#### SPSC queue using atomic size (lock-free, wait-free, with appropriate memory order)

```cpp
array<Item, SIZE> Q;                    |  // Q[0, N) is filled
atomic<size_t> N;                          // count of items
/* Producer */                          |  /* Consumer */
  produce(Q[N]);                           /* write after end of queue */
{                                       |  {
  N.fetch_add(1, memory_order_release); |    while (N.load(memory_order_acquire) <= i);
}                                       |  }
                                        |  consume(Q[i]) // ok to use [0, N)
```

#### Release order
```cpp
thread_A()      |   thread_B()
{               |   {
a += 1;         |   a += 1;   // can not go after release barrier
b += 1;         |   b += 1;   // can not go after barrier
... release barrier ...
c += 1;         |   c += 1;   // it is possible for this line to show up before release barrier
}               |   }
```

#### Acquire order
```cpp
thread_A()      |   thread_B()
{               |   {
a = x;          |   a = x;   // it is possible for this line to show up after acquire barrier
... acquire barrier ...
b = y;          |   b = y;   // can not go before acquire barrier
c = z;          |   c = z;   // can not go before barrier
}               |   }
```

### Compare and swap CAS (lock-free, but not wait-free)

#### Multiply operation in assembly is not atomic

```cpp
std::atomic<size_t> count;

size_t count_copy = count.load(memory_order_relaxed);  // there is no data dependency so can be relaxed
while (!count.compare_and_swap_strong(count_copy, count_copy*10, memory_order_relaxed, memory_order_relaxed))
{}
```

## Thread-safe Singleton, Double checked locking

Scott Meyers singleton, guaranteed thread safe by compiler. Fastest, easiest, best option

```cpp
class Singleton       // Scott Meyer's singleton
{
  Singleton() = default;
  // delete copy, move ctor, dtor, assignment operators
public:
  static Singleton& GetInstance() {
    static Singleton instance;
    return instance;
  }
};
```

Singleton using optional, call_once / once_flag

```cpp
#include <mutex>
#include <optional>
class Singleton
{
public:
  static Singleton* GetInstance();

private:
  Singleton() = default;
  static optional<Singleton> instance;
  static once_flag flag;
};

optional<Singleton> Singleton::instance;
once_flag Singleton::flag {};

Singleton* Singleton::GetInstance()
{
  call_once(flag, []() { instance.emplace(Singleton {}); });
  return &(*instance);
}
```

Singleton with double checked locking
```cpp
#include <atomic>
#include <mutex>
class Singleton
{
public:
  static Singleton* GetInstance();

private:
  Singleton() = default;
  static atomic<Singleton*> instance;
  static mutex mut;
};

atomic<Singleton*> Singleton::instance;
mutex Singleton::mut;

Singleton* Singleton::GetInstance()
{
  Singleton* p = instance.load(memory_order_acquire);
  if (p == nullptr) {
    lock_guard g(mut);
    p = instance.load(memory_order_relaxed);
    if (p == nullptr) {
      p = new Singleton();
      instance.store(p, memory_order_release);
    }
  }
  return p;
}
```

## Data Strucutures
### Thread safe stack

#### Problematic interface

Each member function is thread safe, but together they can't ensure correctness.

```cpp
struct NaiveMTStack {       |  NaiveMTStack s;
  void push(T v);           |  ...
  void pop();               |  if (!s.empty()) {
  T top() const;            |    x = s.top(); // undefined behavior if empty
  bool empty() const;       |    s.pop();
};                          |  }
```

#### Better interface

```cpp
struct MTStack {            |  MTStack s;
  void push(T v);           |  ...
  optional<T> pop();        |  if (!s.empty()) {
  optional<T> top() const;  |    x = s.pop();  // not undefined even if empty
  bool empty() const;       |  }
};                          |
```

#### Locked stack

```cpp
#include <stack>
template<typename T, typename MutexType=mutex>      |  template<typename T>
struct LockedMTStack {                              |  struct UnsafeStack {
  void push(const T& v) {                           |    void push(const T& v) {
    lock_guard g(mut);                              |      s.push(v);
    s.push(v);                                      |    }
  }                                                 |
  optional<T> pop() {                               |    optional<T> pop() {
    lock_guard g(mut); /* writer lock */            |      if (s.empty()) { return optional<T>(nullopt); }
    if (s.empty()) { return optional<T>(nullopt); } |      else {
    else {                                          |        optional<T> v(move(s.top()));
      optional<T> v(move(s.top()));                 |        s.pop();
      s.pop();                                      |        return v;
      return v;                                     |      }
    }                                               |    }
  }                                                 |
  optional<T> top() const {                         |    optional<T> top() const {
    lock_guard g(mut); /* reader lock */            |      if (s.empty()) { return optional<T>(nullopt); }
    if (s.empty()) { return optional<T>(nullopt); } |      else {
    else {                                          |        optional<T> v(s.top());
      optional<T> v(s.top());                       |        return v;
      return v;                                     |      }
    }                                               |    }
  }                                                 |
private:                                            |  private:
  stack<T> s;                                       |    stack<T> s;
  mutable MutexType mut;                            |
};                                                  |  };
```

Performance of `LockedMTStack` vs `UnsafeStack` with 1 thread is 33ns vs 2ns.

A few ideas for performance:
- Provide interface to add / remove batches of items. That will amortize locking cost over N items
- Use RW Lock, `top()` would use R, but `pop()` and `push()` would be W lock. Not much gain in performance in benchmarks

### Thread Safe Queue

#### Option 1 -- spinlock
```cpp
template<typename T>
struct MTQueue {
  void push(const T& v) {
    lock_guard g(l);                // faster than mutex
    q.push(v);
  }

  optional<T> pop() {
    lock_guard g(l);
    if (q.empty()) {
      return optional<T>(nullopt);
    }
    else {
      optional<T> res(move(q.front()));
      q.pop();
      return res;
    }
  }
private:
  queue<T> q;
  mutable spinlock l;
};
```

#### Option 2 -- lock-free, wait-free queue SPSC (1 producer, 1 consumer)

- Producer, Consumer for a queue don't interact unless when the queue is empty. Don't need synchronization, except for `size`, which we can make atomic
- Even alternating `push()`, `pop()` will run out of a linear array when we reach the end. Solution: circular buffer
- Upper bound on the size of the queue
- 1 P, 1 C -- for  transfer data, with very low, predictable latency

```cpp
template<typename T>
struct SPSCLockFreeWaitFreeQueue {
  explicit SPSCLockFreeWaitFreeQueue(size_t cap) : capacity(cap), buffer(new T[cap]) {}
  ~SPSCLockFreeWaitFreeQueue() { delete[] buffer; }

  bool push(const T& v);
  optional<T> pop();
private:
  const size_t capacity;
  T* const buffer;
  size_t front = 0;
  size_t back = 0;
  atomic<size_t> size;
};

bool push(const T& v) {
  if (size.load(memory_order_relaxed) >= capacity) {
    return false;
  }
  new (&(buffer[back % capacity])) T(v);  // placement new
  ++back;
  size.fetch_add(1, memory_order_release);
  return true;
}

optional<T> pop() {
  if (size.load(memory_order_acquire) == 0) {
    return optional<T>(nullopt);
  }
  else {
    optional<T> res( move(buffer[front%capacity]) );
    buffer[front%capacity].~T();
    ++front;
    size.fetch_sub(1, memory_order_relaxed);
    return res;
  }
}
```

## Coroutines in C++20

### Bare c++
```cpp
// g++ -std=c++20 -fcoroutines
#include <coroutine>

// can call the return type anything else, instead of generator<T>
generator<int> a_coroutine_func()
{
  ...
  for (int i = 0; i < 100; ++i)
  {
  co_yield i;
  }
  // or
  // co_await;
  ...
  co_return;
}

int main()
{
   auto handle = a_coroutine_func().h_;     // creates activation frame
   auto& promise = handle.promise();        // not std::promise, a different type, generator::promise_type
   ...
   promise.value_;          // use what yield returned
   handle();                // resume the coroutine, like next() in python
   ...
   handle.destroy();
}

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

## Build Catch2 unittests

### Catch2 - Build local copies from GIT repo
```text
git clone https://github.com/catchorg/Catch2.git
cd Catch2

cmake . -B build-debug -DCMAKE_BUILD_TYPE=Debug -G Ninja -DBUILD_TESTING=off -DCMAKE_INSTALL_PREFIX=d:/devtools/catch2
cmake --build build-debug --target install

cmake . -B build-release -DCMAKE_BUILD_TYPE=Release -G Ninja -DBUILD_TESTING=off -DCMAKE_INSTALL_PREFIX=d:/devtools/catch2
cmake --build build-release --target install
```

### Catch2 - Example CMakeLists.txt file

Top level
```text
cmake_minimum_required(VERSION 3.22)
project(TBD_Project_Name VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)

include_directories(${PROJECT_SOURCE_DIR}/include)

add_subdirectory(src)
add_subdirectory(example)

if (NOT DISABLE_CATCH2)
    if (Catch2_ROOT)
        find_package(Catch2 REQUIRED) # define Catch2_ROOT=d:/devtools/catch2
    else()
        include(FetchContent)
        FetchContent_Declare(Catch2 GIT_REPOSITORY https://github.com/catchorg/Catch2.git GIT_TAG v3.5.0)
        FetchContent_MakeAvailable(Catch2)
        list(APPEND CMAKE_MODULE_PATH ${catch2_SOURCE_DIR}/extras)
    endif()

    add_subdirectory(tests)

    include(CTest)
    enable_testing()
endif()

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
```

Test directory

```text
include(CTest)
include(Catch)

set (AllTheTests mytest1)

add_executable(mytest1 mytest1.cpp)

foreach (test ${AllTheTests})
    target_link_libraries(${test} PRIVATE disruptor Catch2::Catch2WithMain)
    catch_discover_tests(${test}) # will take care of -- add_test(NAME ${test} COMMAND ${test})
endforeach()
```


### Catch2 - Build your code
```bash
cmake . -B build-debug -D CMAKE_BUILD_TYPE=Debug -D Catch2_ROOT=d:/devtools/catch2 -G Ninja
cmake --build build-debug --target all
ctest --test-dir build-debug
```

### Catch2 - Example test code

```cpp
#include <catch2/catch_test_macros.cpp>

TEST_CASE( test_name, "[tagname]" ) {
  // setup, will execute once for each SECTION() below
  ... some setup code ...

  ... some checks to verify setup ...
  REQUIRE(condition1);
  CHECK(condition2);
  REQUIRE_FALSE(condition3);
  CHECK_FALSE(condition3);
  REQUIRE_NOTHROW(expression);
  REQUIRE_THROWS(expression);
  REQUIRE_THROWS_AS(expression, exception_type);
  REQUIRE_THROWS_WITH(expression, string_or_matcher);
  REQUIRE_THAT(expression, Matcher);

  SECTION( section1_name ) {
    ...
    REQUIRE(condition1_1);
    ...
    SECTION( nested_section1_1_name ) {
      ...
      REQUIRE(condition1_1_1);
      ...
    }
  }
}

// benchmarking
#include <catch2/benchmark/catch_benchmark.hpp>

TEST_CASE( test_name, ... ) {
  BENCHMARK( "benchmark 1" ) {
    ... some_time_consuming_code ...
    return some_value;
  };
}
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
- TCMalloc thread caching malloc

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
- Thread Sanitizer in GCC, Clang - detects data races etc
- NUMA - Non Uniform Memory Architecture - a memory bank is closer to one CPU, memory is not symmetric
- SIMD instructions -- SSE, AVX
- RCU Read-Copy-Update synchronization mechanism

## Glossary
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

- Compiler Optimizations
  - RVO return value optimization, NRVO named-RVO
  - Copy elision, Move elision
  - Loop unrolling
  - Strength reduction - taking expensive operations and transforming them to less expensive
  - Inlining
  - Constant folding - replace expressions that can be calculated at compile time with constant
  - Constant propagation - value is constant for all possible executions
  - Dead code removal
  - Instruction selection - set of choices of assembly instructions to choose
    - `countSetBits(n)` -> `POPCNT`
    - https://uops.info/table.html
  - Loop invariant code movement
  - Peephole optimization - look for local optimizations between short sequences of instructions
  - Tail call removal - replace recursive function calls with a loop
  - LTO link time optimization, LTCG link time code generation, `g++ -flto a.cpp b.cpp -o main`
  - Devirtualization, at LTO time, speculative devirtualization

- C++ Idioms
  - Empty base class optimization
  - CRTP
  - RAII
  - Tag dispatching
  - Type erasure

## Latency numbers

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

- Ref: Rocket Lake, 11th Gen Intel Core i7 11700 @ 2.5GHz, Cores 8, Threads 16, 32 GB, L1 32KB, L2 2MB, L3 6MB, PCIe 4
- Ref: Alder Lake, Intel Core i3-N305 @ 1.8 GHz, Core 8, Threads 8, 8 GB, L1 48KB, L2 512KB, L3 16MB, PCIe 3,

### Create Shortcut on windows
```text
C:\tools\cmder\current\vendor\git-for-windows\mingw64\bin\create-shortcut.exe

create-shortcut "PATH_TO_SOURCE" "PATH_TO_DESTINATION"

Usage: %s [options] <source> <destination>
  options:
  --work-dir  DIR_PATH
  --arguments EXTRA_ARGS
  --show-cmd "Normal window" "Minimised" "Maximised"
  --icon-file ICON_FILE_PATH
  --description "SOME COMMENT STRING"
  --desktop-shortcut
  --dry-run

also:

nircmd shortcut PATH_TO_SOURCE DEST_FOLDER DEST_FILENAME

nircmd shortcut [filename] [folder] [shortcut title] \
  {arguments} {icon file} {icon resource number} \
  {ShowCmd} {Start In Folder} {Hot Key}

Creates a shortcut to a file.

The parameters:

  [filename]: Create a shortcut to this filename.
  [folder]: Specify the destination folder that inside it the shortcut will be created. You can specify any valid folder, including the special variables that represent system folders, like ~$folder.desktop$ (Desktop folder), ~$folder.programs$ (Start-Menu-Programs folder), and so on...
  [shortcut title]: The text displayed in the shortcut.
  {arguments}: Optional parameter - Additional arguments to execute the filename.
  {icon file}: Optional parameter - Use this parameter if your want that the shortcut will be displayed with icon other than the default one.
  {icon resource number}: Optional parameter - The resource number inside the icon file.
  {ShowCmd}: Optional parameter - Use this parameter if you want to maximize or minimize the window of the program. Specify "max" to maximize the window or "min" to minimize it.
  {Start In Folder}: Optional parameter - Specifies the "Start In" folder. If you don't specify this parameter, the "Start In" folder is automatically filled with the folder of the program you specify in [filename] parameter.
  {Hot Key}: Optional parameter - Specifies an hot-key that will activate the shortcut. For example: Alt+Ctrl+A, Alt+Shift+F8, Alt+Ctrl+Shift+Y

Examples:
shortcut "f:\winnt\system32\calc.exe" "~$folder.desktop$" "Windows Calculator"
shortcut "f:\winnt\system32\calc.exe" "~$folder.programs$\Calculators" "Windows Calculator"
shortcut "f:\Program Files\KaZaA\Kazaa.exe" "c:\temp\MyShortcuts" "Kazaa"
shortcut "f:\Program Files" "c:\temp\MyShortcuts" "Program Files Folder" "" "f:\winnt\system32\shell32.dll" 45
shortcut "f:\Program Files" "c:\temp\MyShortcuts" "Program Files Folder" "" "" "" "max"
See: https://www.nirsoft.net/utils/nircmd2.html
```

# Command line
### Zoxide
```text
zoxide query -a -l -s
```

### Start VM
```
"c:\Program Files\Oracle\VirtualBox\VBoxManage" startvm jammy-ubuntu --type headless
```

### Export GIT repository
```
git daemon --reuseaddr --informative-errors --verbose --export-all --enable=receive-pack --base-path=C:\repos

> git clone git://localhost/dotfiles
```

### Readonly GIT repository
```
git daemon --reuseaddr --informative-errors --verbose --export-all --base-path=C:\repos
```

### MinTTY Terminal Bash
```
vendor\git-for-windows\usr\bin\bash --login -i
vendor\git-for-windows\usr\bin\mintty /bin/bash -l

PowerShell -ExecutionPolicy Bypass -NoLogo -NoProfile -NoExit -Command "Invoke-Expression 'Import-Module ''vendor\profile.ps1'''"
```

### Veracrypt
```
veracrypt /volume filename /letter t /password "password" /hash sha512 /wipecache /cache n /quit /silent
veracrypt /v filename /l t /p "password" /hash sha512 /w /c n /q /s

veracrypt /dismount /letter t /force /quit
veracrypt /d /l t /f /q

# https://www.veracrypt.fr/en/Command%20Line%20Usage.html
```

### Music download
```
mpv playlist.m3u

yt-dlp -x url -o "blah.ogg"             # extract-audio
yt-dlp --extract-audio --audio-quality 0 --audio-format opus url
# other useful flags: --no-mtime -o "%(title)s.%(ext)s"
# audio formats: best aac, alac, flac, m4a, mp3, opus, vorbis, wav
# audio quality: 0 (best), 10 (worst)
# https://github.com/yt-dlp/yt-dlp
```

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

# Design Patterns

## DP - Creational - Factory Method - Identifier

```cpp
enum class ProductId { A, B, C, D, };

// interface for the object to be created
class Product {
public:
  virtual ~Product() = default;
  virtual void foo() = 0;
};

// concrete classes, whose objects will get created by the factory
class ProductA : public Product {
public:
  void foo() override { ... }
};
class ProductB : public Product {
public:
  void foo() override { ... }
};
...

// class with the factory method
class Creator {
public:
  unique_ptr<Product> createProduct(ProductId id) {
    switch (id) {
    case ProductId::A:
      return make_unique<ProductA>();
    case ProductId::B:
      return make_unique<ProductB>();
    ...
    }
    return nullptr;
  }
};
// alternatively, could have a base Creator interface class and a concrete derived Creator with a factory method

// using factory method pattern
unique_ptr<Creator> creator = make_unique<Creator>();
auto product = creator->createProduct(ProductId::D);
product->foo();
```

class diagram

```mermaid
classDiagram
direction TB

class Product {
  <<interface>>
  + dtor()*
  + foo()*
}

class ProductA {
  + foo()
}

class ProductB {
  + foo()
}

Product <|-- ProductA
Product <|-- ProductB

class Creator {
  + createProduct(id : ProductId) ProductPtr
}
```

## DP - Creational - Factory Method - Inheritance

Create objects without having to specify the exact class of the object that will be created. Define a separate operation `factoryMethod` for creating an object. Defer instantiation to subclasses.

```mermaid
classDiagram
direction TB

class Product {
  <<interface>>
  + dtor()*
  + foo()*
}

class ProductA {
  + foo()
}

class ProductB {
  + foo()
}

Product <|-- ProductA
Product <|-- ProductB

class ICreator {
  <<interface>>
  - makeProduct()*
  + createProduct()
}

class Creator1 {
  - makeProduct()
}
ICreator <|-- Creator1
Creator1 ..> ProductB : creates
```

```cpp
// interface for the object to be created
class Product {
public:
  virtual ~Product() = default;
  virtual void foo() = 0;
};

// concrete classes, whose objects will get created by the factory
class ProductA : public Product {
public:
  void foo() override { ... }
};
class ProductB : public Product {
public:
  void foo() override { ... }
};
...

// Base Class
class ICreator {
protected:
  virtual unique_ptr<Product> makeProduct() = 0;

public:
  unique_ptr<Product> createProduct() { // factory method
    return makeProduct();     // defined in a derived class
  }

  unique_ptr<ComplexProduct> createComplex() { // factory method
    auto a = makeProduct();    // complex product consists of 2 products
    auto b = makeProduct();
    return make_unique<ComplexProduct>(a, b);
  }
};

class CreatorA : public ICreator {
protected:
  unique_ptr<Product> makeProduct() override {
    return make_unique<ProductA>();
  }
};

class CreatorB : public ICreator {
protected:
  unique_ptr<Product> makeProduct() override {
    return make_unique<ProductB>();
  }
};

// using factory method pattern
unique_ptr<ICreator> creator = make_unique<CreatorA>();
auto product = creator->createProduct();
product->foo();

auto complex = creator->createComplex();
complex->blah();
```

## DP - Creational - Abstract Factory

create families of related objects without specifying their concrete classes. encapsulating a group of individual factories

```cpp
// abstract base
class MapSite {
public:
  virtual void enter() = 0;
  virtual ~MapSite() = default;
};

// concrete objects to be created
class Room : public MapSite {
  int roomNumber;
public:
  Room(int n) : roomNumber(n) {}
  void setSide(Direction d, MapSite* site) { ... }
  void enter() override {}

  Room(const Room&) = delete;
  Room& operator=(const Room&) = delete;
};

class Wall : public MapSite {
public:
  void enter() override {}
};

class Door : MapSite {
  Room* room1;
  Room* room2;
public:
  Door(Room* a, Room* b) : room1(a), room2(b) {}
  void enter() override {}
};

class Maze : public MapSite {
public:
  void addRoom(Room* r);
  Room* getRoom(int idx) const;
  void enter() override {}
};

// abstract factory base
class IMazeFactory {
public:
  virtual Room* createRoom(int id)            = 0;
  virtual Wall* createWall()                  = 0;
  virtual Door* createDoor(Room* a, Room* b)  = 0;
  virtual Maze* createMaze()                  = 0;
  virtual ~IMazeFactory()             = default;
};

// concrete factory class
class MazeFactory : public IMazeFactory {
public:
  Room* createRoom(int id)            override { return new Room(id); }
  Wall* createWall()                  override { return new Wall(); }
  Door* createDoor(Room* a, Room* b)  override { return new Door(a, b); }
  Maze* createMaze()                  override { return new Maze(); }
};

// client using abstract factory
class MazeGame {
public:
  Maze* createGame(IMazeFactory& factory) {
    // create some rooms, walls, doors, add them a maze
    Maze* maze = factory.createMaze();
    Room* r1 = factory.createRoom(1);
    Room* r2 = factory.createRoom(2);
    Door* aDoor = factory.createDoor(r1, r2);
    aMaze->addRoom(r1);
    aMaze->addRoom(r2);
    r1->setSide(North, factory.createWall());
    r1->setSide(East, aDoor);
    r1->setSide(South, factory.createWall());
    r1->setSide(West, factory.createWall());
    r2->setSide(North, factory.createWall());
    r2->setSide(East, factory.createWall());
    r2->setSide(South, factory.createWall());
    r2->setSide(West, aDoor);
    return maze;
  }
};

MazeGame game;
MazeFactory factory;
game.createGame(factory);
```

class diagram

```mermaid
classDiagram
direction TB

class Product1 {
  <<interface>>
  + dtor()*
  + foo()*
}

class Product1A {
  + foo()
}

Product1 <|-- Product1A

class Product2 {
  <<interface>>
  + dtor()*
  + bar()*
}

class Product2A {
  + bar()
}

Product2 <|-- Product2A

class AbstractCreator {
  <<interface>>
  + createProduct1() Product1Ptr*
  + createProduct2() Product2Ptr*
}

class CreatorA {
  + createProduct1() Product1Ptr
  + createProduct2() Product2Ptr
}

AbstractCreator <|-- CreatorA

CreatorA ..> Product2A : creates
CreatorA ..> Product1A : creates
```

## DP - Creational - Builder

assemble a complex object from its parts, encapsulates internal representation & construction steps of the complex object


```mermaid
classDiagram
direction TB

class Product1 {
  + foo()
}

class Product2 {
  + bar()
}

class AbstractBuilder {
  <<interface>>
  + reset()*
  + buildStep1()*
  + buildStep2()*
}

class Builder1 {
  + reset()
  + buildStep1()
  + buildStep2()
  + getResult() : Product1
}

AbstractBuilder <|-- Builder1

Builder1 ..> Product1 : creates

class Builder2 {
  + reset()
  + buildStep1()
  + buildStep2()
  + getResult() : Product2
}

AbstractBuilder <|-- Builder2

Builder2 ..> Product2 : creates

class Director {
  - builder : AbstractBuilder
  + CTor(builder)
  + changeBuilder(builder)
  + make(type)
}
```

```cpp
struct Car {
  GPS gps;
  TripComputer tripComputer;
  Engine engine;
  Seats seats;  
};

struct UserManual {
  Pages pages;
};

struct IBuilder {
  virtual void reset() = 0;
  virtual void setSeats(...) = 0;
  virtual void setEngine(...) = 0;
  virtual void setTripComputer(...) = 0;
  virtual void setGPS(...) = 0;
};

class CarBuilder : public IBuilder {
  unique_ptr<Car> car;
public:
  CarBuilder() {
    reset();
  }
  void reset() override {
    car = make_unique<Car>();
  }
  void setSeats(...) override {
    car->seats.update(...);
  }
  void setEngine(...) override {
    car->engine.set(...);
  }
  void setTripComputer(...) override {
    car->tripComputer.set(...);
  }
  void setGPS(...) override {
    car->gps.set(...);
  }
  unique_ptr<Car> getResult() {
    unique_ptr<Car> result = car;
    car.reset();
    return result;
  }
};

class UserManualBuilder : public IBuilder {
  unique_ptr<UserManual> manual;
public:
  UserManualBuilder() {
    reset();
  }
  void reset() override {
    manual = make_unique<UserManualBuilder>();
  }
  void setSeats(...) override {
    manual->pages.describeSeats(...);
  }
  void setEngine(...) override {
    manual->pages.describeEnginet(...);
  }
  void setTripComputer(...) override {
    manual->pages.describeTripComputer(...);
  }
  void setGPS(...) override {
    manual->pages.describeGPS(...);
  }
  unique_ptr<UserManual> getResult() {
    unique_ptr<UserManual> result = manual;
    manual.reset();
    return result;
  }
};

class Director {
public:
  void assembleSedan(IBuilder& builder) {
    builder.reset();
    builder.setSeats(5);
    builder.setEngine(new OrdinaryEngine);
    builder.setTripComputer(true);
    builder.setGPS(false);
  }
  void assembleSportsCar(IBuilder& builder) {
    builder.reset();
    builder.setSeats(2);
    builder.setEngine(new SportEngine);
    builder.setTripComputer(true);
    builder.setGPS(true);
  }
};

class Customer {
public:
  tuple<unique_ptr<Car>, unique_ptr<UserManaul>> makeCarWithUserManual() {
    Director director;

    CarBuilder car_builder;
    director.assembleSportsCar(car_builder);
    auto my_car = car_builder.getResult();

    UserManualBuilder manual_builder;
    director.assembleSportsCar(manual_builder);
    auto my_user_manual = manual_builder.getResult();
    return make_tuple(my_car, my_user_manual);
  }
};
```

## DP - Creational - Prototype

clone to produce new objects
```mermaid
classDiagram
direction TB

class IProduct {
  <<interface>>
  + clone() IProduct*
}

class Product1 {
  + clone() Product1
}

IProduct <|-- Product1

class Client

Client ..> Product1 : clone

```

```cpp
class MapSite {
public:
  virtual MapSite* clone() const = 0;
};

class Room : public MapSite {
public:
  Room* clone() const override {
    return new Room(*this);
  }
};

class IMazeFactory {
public:
  virtual Room* makeRoom(int n) const = 0;
};

class MazePrototypeFactory : public IMazeFactory {
  Room* modelRoom;
public:
  MazePrototypeFactory(Room *r) : modelRoom(r) {}

  Room* makeRoom(int) const override {
    return modelRoom->clone();
  }

  ...
};

MazeGame game;
MazePrototypeFactory factory(new Room(1));
game.createGame(factory);
```

## DP - Creational - Singleton

Check out Scott Meyers singleton implementation

## DP - Creational - RAII
## DP - Creational - Object Pool
## DP - Creational - Multiton
## DP - Creational - Lazy Initialization
## DP - Creational - Dependency Injecton

- Service - contains some useful functionality
- Client - uses services
- Dependencies - services required by a client
- Interfaces - clients do not know how the services / dependencies are implemented. Only the API. Clients do not need to change when implementation of  services changes.
- Injector / Assembler / Container / Provider / Factory - introduces services to the client. Construct and connect clients and services, may be a complex object graph. No circular dependencies.

```cpp
class IService {
public:
};

class Client {
  IService* service;
public:
  Client(IService* svc) : service(svc) {}

  void setService(IService* svc) { service = svc; }

  void foo();
};

class ExampleService : public IService {
public:
};

IService* service = new ExampleService();
Client client = new Client(service);

client.foo();
```

- Separate the concerns of constructing objects and using them
- Loosely coupled programs
- Client does not construct the Services
- Dependency inversion principle
- Inversion of control - framework first constructs an object, then passes control flow to it

## DP - Structural - Adapter



## DP - Structural - Bridge
## DP - Structural - Composite
## DP - Structural - Decorator
## DP - Structural - Facade
## DP - Structural - Flyweight
## DP - Structural - Proxy

## DP - Behaviroal - Chain of responsibility
## DP - Behaviroal - Command
## DP - Behaviroal - Interpreter
## DP - Behaviroal - Iterator
## DP - Behaviroal - Mediator
## DP - Behaviroal - Memento
## DP - Behaviroal - Observer
## DP - Behaviroal - State
## DP - Behaviroal - Strategy
## DP - Behaviroal - Template method
## DP - Behaviroal - Visitor

## SOLID
- Single Responsibility - "Responsibility" means "Reason for change". A module should have only 1 responsibility, so that if it changes, it should change for 1 reason. If it has 2 responsibilities / roles, it may change if any of them changes.
- Open-Closed - interface should be open for extension, closed for modification. **Modifying an API may break existing code that uses the API. Extending the API does not break.**
- Liskov Substitution - if D derives from B, then wherever we can use B, we should be able to substitute with D. **Ok to substitute DERIVED in-place of BASE**
- Interface Segregation - split very large interfaces into smaller, more specific ones. So that a client object depends on a service object interface that has only the methods that the client uses. **SMALL RELEVANT INTERFACES**
- Dependency Inversion - high level abstractions (interfaces) **do not** depend on (concrete) low level details. Instead "details" / "concrete implementations" should depend on "abstractions" / "interfaces". **INTERFACES DO NOT DEPEND ON IMPLEMENTATION**


## Design goals
- Loose coupling
- Tight cohesion
- Separation of concerns
- Encapsulation
- Information hiding / Data hiding
- IoC Inversion of Control - Like a callback. Don't call us, we will call you / Hollywood principle. Unlike procedural programming, where user code calls library functions. In a callback mechanism, user code gets called to handle something. Inverted from procedural paradigm. Event loop, web server frameworks, dependency injection use IoC