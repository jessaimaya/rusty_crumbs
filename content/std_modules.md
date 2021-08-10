+++
title="Rust Standard Library Modules"
description="RSL Modules Diagram"
date=2021-08-10
draft = false

[taxonomies]
tags = [ "rust", "std", "diagram", "no-code"]
categories = ["no-code", "diagrams", "notes"]

[extra]
+++

A quick diagram representing modules on `std::`
We can group them in: `SysCalls  Oriented` & `Computation Oriented`

## Syscalls-Oriented
Modules that manage system hardware resources. (kernel required for privileged ops)
<div class="mermaid">
 classDiagram
    class Concurrency{
        env
        sync
        process
        thread
    }
    class Networking {
        net
    }
    class IO {
        IO
    }
    class OS Specific {
        OS
    }
    class Time Related {
        time
    }
    class Async {
        future
        task
    }
    class FileSystem {
        fs
        path
    }
    class MemoryManagement {
        alloc
        convert
        ptr
        borrow
        default
        rc
        cell
        mem
        clone
        pin
    }
</div>

## Computation-Oriented
Data representation, computation and instructions to the compiler.
<div class="mermaid">
 classDiagram
    class DataProcessing {
        ascii
        fmt
        num
        cmp
        hash
        ops
        iter
    }
    class ErrorHandling {
        error
        panic
        option
        result
    }
    class Compiler {
        hint
        primitive
        prelude
    }
    class ffi {
        ffi
    }
    class DataTypes {
        any
        f32
        marker
        string
        array
        f64
        slice
        str
        vec
        char
        i8..isize
        u8...usize
        collections
    }
    
</div>

### Notes
For the tricky ones:
- **Cell:** Memory safety is based on the rule that a value can have either several immutable references to it a single mutable reference. On scenarios where a shared mutable reference is required.
- **Clone:** primitive types such as integers are _copyable_. Not all types can be copied, because they may require memory allocation; example: `String` or `Vec` types memory are allocated in the heap, rather than the stack. In such cases, a `clone()` method is used to duplicate a value.
- **Convert:** conversion between data types
    - **AsRef:** by implementing this trait we can write a function that takes a parameter of type `AsRef<str>`, which means that this function can accept any reference that can be converted into a string reference `(&str)`
- **Pin:** types in rust are _movable_ by default. For example `Vec` type, a `pop()` operation moves a value out and a push operation may result in the reallocation of memory. However, there are situations where it is useful to have objects with fixed (_pinned_) memory locations (_linked-lists_).
- **ptr:** Rust support two types of raw pointers
  - **\*const i32:** immutable
  - **\*mut i32:** mutable
- **rc:** (_reference-counted_): single-threaded reference-counting pointers. A reference-counted pointer to an object of type `T` can be represented as `Rc<T>`. This provides shared ownership of value `T`, which is allocated in the heap. If it is cloned, a new pointer to the same memory location in the heap is returned (_does not duplicate the value in memory_).
- **sync:** synchronization of primitives are needed to coordinate operations across threads. Here are primitives such as `Arc` - `Mutex` - `RwLock` - `Condvar`.
- **[prelude v1](https://doc.rust-lang.org/std/prelude/index.html)** items included in every rust program.


<div class="footnotes">
  <div class="footnote">
    <span class="highlight">Source:</span> <a target="_blank" title="Practical System Programming for Rust Developers" href="https://www.amazon.com.mx/Practical-System-programming-Rust-developers/dp/1800560966">Practical System Programming for Rust Developers</a>
  </div>
</div>