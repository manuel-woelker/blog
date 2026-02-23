
---
title: "I Wish I Had a Hot-Reloading Compiler"
date: 2026-02-23T06:01:31+01:00
draft: true
tags: ["documentation"]
categories: []
description: "Hypothesis: Compilers should compile and hot-reload code as soon as I save it."
author: "Manuel Woelker"
showToc: true
---

## What is wrong with the current compile lifecycle?

**It is slow.** When developing, I value fast feedback. *Immediate* feedback. The faster I can see where my code is broken, the faster I can fix it.

But currently there's a 3-step process for this feedback:

1. Modify code
2. Run Checks/Lints/Tests or examples
3. Apply fixes

Step 2 is usually the time-consuming part, since it requires compiling the code, linking it, running the tests, etc. This breaks my development flow.

## How could it be better?

Typechecking inside the IDE is great because it is so *immediate*: As soon as I type in something wrong, the IDE will show me an error, and I can fix it right away.

**We can have the same immediate feedback for my tests, and for the actual program execution.**

As soon as I hit Ctrl+S, the compiler should compile the code (*and only the code 
that actually needs to be compiled*), run the tests (*and only the tests that might be affected by the code change*), and give me feedback about test failures.

There are some tools and IDE plugins that support this workflow, but as far as I know, they are not as deeply integrated with the compiler. Incremental 
compilation and smart test execution, is a key requirement to make this fast. 

The same goes for the actual program: I want the program to either:

1. Patch the running program with the new code **while it is running**
2. Or, if that is not possible, restart the program with the new code, and **get it into the same program state**

## How could this be implemented?

Here's how this could work in practice:

1. **The compiler is running as a daemon**: Rather than being invoked and having to start from scratch, the compiler is running continuously, and watches 
   for filesystem changes. Once it detects those, it recompiles and reruns the tests and/or the program. Now *that* is true Ahead-Of-Time compilation.
2. **Incremental compilation**: To make compilation fast, the compiler must do the minimum amount of work. The way to do this is with a query driven 
   compilation, where a lot of the compilation work is cached/memoized, and dependencies are finely tracked to prune redundant work.
3. **Smart test execution**: To make test execution fast, the compiler must only run the tests that might be affected by the code change. This can be 
   done by tracking dependencies between code and tests, and only running the tests that are affected by the code change.
4. **Function hot-reloading**: To apply the code changes to the running program, we need to inject it into the running program. For interpreted or bytecode 
   based environment this should be fairly simple. For *native* code it seems a bit more complex, but should be doable with a trampoline mechanism or a 
   dispatch table. It would probably require a custom linker to support that.
5. **State-aware program re-execution**: In cases where function patching is not possible (e.g. because of signature or memory layout changes), I'd like the 
   program to be terminated, restarted with the new code, and *ideally* somehow brought into the same program state.

The last part might require some support from program itself, e.g. a way to snapshot and load the program state or the inputs. For terminal programs this might 
be as simple as recording and replaying keystrokes.

## What are the benefits of this approach?

1. **Immediate feedback**: As soon as I hit Ctrl+S, I get all feedback about test failures and program errors.
2. **Integration with LSPs**: The compiler might flag the issues directly in the IDE using LSPs.
3. **Less waiting**: Even without all the fancy integration, having the hard work of compilation already done means that as soon as I want to 
   execute the program, it is already ready to go, thanks to the "true" Ahead-Of-Time compilation.
4. **Better feedback loops for LLMs**: With Coding-Agents becoming better and faster, the compilation and test step might become an even bigger timesink or 
   bottleneck. It seems kinda bonkers to me that running a terabyte+ model with billions of matrix operations is the *fast* part, and the deterministic, 
   mostly linear compilation step is the *slow* part.
5. **Faster CI**: Fine-grained incremental compilation with persistent caching and smart test execution means that CI can be much faster, and used more 
   efficiently.

## What am I doing about it?

I am currently working on a proof-of-concept compiler that supports this approach. It is called [holo](https://github.com/manuel-woelker/holo).

The goal of this proof-of-concept is to answer the following questions:

1. Is it viable to implement this approach in a understandable, performant and safe way?
2. Does it actually bring any value? 

*Full disclosure:* \
I had Codex review this post before publishing. The text was all written by an organic neural network (i.e. me). All errors and omissions are entirely my own.