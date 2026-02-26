
---
title: "I wish I had a language that lets me prevent certain functions to have certain effects"
date: 2026-02-26T19:31:21+01:00
draft: false
tags: ["compiler", "effects"]
categories: []
description: "An idea for an effect type system, that allows preventing effects"
author: "Manuel Woelker"
showToc: true
---

## What am I hoping to achieve?

Type systems usually express the input and output types of a function, but not what side effects the function may have.

I want to be able to deny certain side effects in some parts of my code, for safety, correctness or documentation purposes.

## What are some examples of side effects to forbid?

1. **Must not panic**, since that leaves my program in an undefined state.
2. **Must not access the network**, to prevent unwanted calls.
3. **Must not access filesystem**, to prevent reading local data or having slow performance.
4. **Must not *write* to the filesystem**, to prevent causing damage to the persistent system state.
5. **Must not allocate memory**, to prevent memory exhaustion errors for embedded systems.
6. **Must not cause interrupts**, to prevent triple faults in interrupt handlers.
7. **Must not block**, to prevent blocking event threads in async context.
8. **Must not syscall**, to prevent manipulating the system state.
9. **Must not loop**, to prevent unbounded loops making the system unresponsive.
10. **Must not recurse**, to prevent stack overflows.
11. **Must not cause non-determinism**, to make results deterministic and time independent.
12. **Must not branch**, to ensure constant execution time, or better GPU core utilization.
13. **Must not divide**, to prevent division by zero errors.
14. **Must not perform floating point arithmetic**, to ensure financial code does not suffer rounding errors, or that code is portable to low-end CPUs.
15. **Must not spawn threads**, to enforce single-threading.
16. **Must not lock**, useful to ensure and communicate that functions are lock-free.
17. **Must not use atomics**, to ensure that there is no cache contention risk.
18. **Must not use SIMD/vector extensions**, to ensure the code remains portable or doesn't force the CPU into an inefficient processor state.

## What are the benefits of such a system?

There are several benefits to this mechanism:

### Safety

Potentially dangerous behavior can be denied in large parts of the code base, and confined to a smaller section that is easier to reason about or audit.

### Security

The language can deny access to network and filesystem to external dependencies to prevent unauthorized access or supply chain attacks at the type level.

### Documentation

Putting these effects and their restrictions into the language and type systems allows users to better understand the *behavior* of a function, without having to dig into the code.

The compiler ensures that these promises are upheld.

### Correctness

Certain side effects may compromise the correctness of a function. By having the compiler check these invariants, we can provide better correctness guarantees.

### Performance

Knowing that certain effects *cannot* happen may allow the compiler to perform certain optimizations, e.g. omit stack unwinding machinery.

## What could this look like in practice?

There might be two different effect annotations in a language:

1. **`can` annotations** to indicate that a function may exhibit side effects (for cases where this might not be done by the compiler automatically, or we want to reserve the ability to so in the future)
2. **`must not` annotations** to deny a function from having an effect. 

In a fictional programming language:

```rust
fn acquire_lock() can lock {
    ...
}

fn increment_counter() -> i32 must not lock {
    acquire_lock();
    counter += 1;
}
```

This snippet should fail to compile, since the signature forbids locking. This ensures that the contract is upheld.

From an ergonomics perspective it probably makes sense to have the compiler infer some of the effects for functions automatically (at least for private or internal functions), to avoid having to spell them out.

Public functions might need full effect annotations, since this represents the contract of the function. 

## What are the downsides?

1. **Implementation complexity**: The effect checking mechanism may become complex, especially when considering closures as values.
2. **Learning curve**: It might be hard to get started with this concept, which may lead to friction adopting this feature.
3. **Verbose**: Spelling out all the effects may become unwieldy, similar to checked exceptions languages like Java.
4. **Lack of power**: This is a relatively lightweight effect system, but it does not allow "handling" effects further up the stack like some other languages that use things like algebraic effects.

## What am I doing about it?

I am currently working on a proof-of-concept language that intends to add such a feature. It is called [holo](https://github.com/manuel-woelker/holo).

The goal of this proof-of-concept is to answer the following questions:

1. How can such a system be implemented?
2. Is it worth the effort?

Ideally I'd like to see this idea taken up in other languages to make it easier to reason about what functions actually do.

*Full disclosure:* \
I had Codex review this post before publishing. The text was all written by an organic neural network (i.e. me). All errors and omissions are entirely my own.