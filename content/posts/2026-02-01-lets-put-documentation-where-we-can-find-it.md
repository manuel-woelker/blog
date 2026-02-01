---
title: "Let's Put Developer Documentation Where We Can Find It - In the Code"
date: 2026-02-01T06:10:44+01:00
draft: false
tags: ["documentation"]
categories: []
description: "Hypothesis: Putting developer documentation directly into the code should make it easier to find, and easier to keep up to date."
author: "Manuel Woelker"
showToc: true
---

# What's wrong with developer documentation?

I have been thinking a lot lately about developer documentation and from my perspective, there are two main issues with it from my experience:

1. **It's hard to find the relevant documentation for a piece of code.**
2. **The documentation is outdated, and does not reflect the current state of the code**

I feel that often #2 is a direct consequence of #1.

# How do we fix this?

Here's my simple pitch to address these issues:

**Let's put the developer documentation where we can find it: _In the code_**

The underlying premise is that it is easier to find and update this documentation when you can't help but stumble into it. This reduces the barrier of finding it, and makes it more obvious when it needs to be updated.

It also reduces friction for creating *new* documentation, since we can just put it where we are right now.

# What would this look like in practice?

```rust
/* 📖 # Why use a connection pool here?

There may be many threads servicing HTTP requests simultaneously.
Using a connection pool has the following benefits:

1. Reduces database load because there's a fixed number of connections
2. Improves latencies because the connection and authentication
   handshake can usually be omitted
3. In situations of high load, some connection attempts can be
   gracefully denied to allow others to proceed. This is better than
   every thread bombarding the database, which would lead to no request
   making progress and everyone timing out.

*/
let connection_pool = ConnectionPool::new(...)?;
```

I have experimented with using the unicode [📖 symbol](https://graphemica.com/%F0%9F%93%96) to indicate these explainer documentation blocks. I find it makes it easy to find these signposts when scanning code.

If you are more ASCII-minded, something like `DOC:` would work as well.

# Wait, isn't this just normal code comments?

In theory yes, but in practice I have usually seen a lot of developer documentation put into a separate directory (or even a separate repository) making it harder to find, access and update.

The code comments I tend to find are usually more implementation focussed, and less about overarching concerns like architecture, security, performance, etc.

For cross-cutting or "big picture" topics there may not be one source file to put this documentation into, but I think in many cases, putting more of this documentation into the code is better for discoverability and for keeping it up to date.

A good example are architecture decision records (ADRs) - why not put them next to the code that is shaped by this decision? Whenever someone reads or modifies that code, they have the reasoning at hand.
This prevents these decisions being overturned due to ignorance.

# What do you call this?

I have taken to call this "Hyperliterate Programming" in a nod to [Knuth's](https://www.cs.tufts.edu/~nr/cs257/archive/literate-programming/01-knuth-lp.pdf) "[Literate Programming](https://en.wikipedia.org/wiki/Literate_programming)". 

I think of it as "beyond" Literate Programming.

My feeling is that Literate Programming as envisioned by Knuth would not work in most development teams, but I think this approach is a practical step in that direction.

(Aside: I initially wanted to call this "Post-literate Programming", but it turns out "post-literate" is already a concept that has a different meaning and connotation.)

# What are the downsides?

1. **Documentation is sprinkled all over the place** - There is no "one place" to find the documentation. This could be ameliorate with tooling to extract this.
2. **Violation of Separation of concerns** - This may be seen as mixing the concerns of code and documentation. Though I like to think of it as one concern: "Describing how the problem is solved", with parts of this description being readable by a compiler (i.e. the code).
3. **No single source file for cross-cutting concerns**: Some cross-cutting or overarching documentation concepts may not have a clear single place to put it. That's okay - these probably should live in a central location. But it might be a good idea to cross-reference those at the the relevant places in the source code.
4. **The development team needs to be onboard** - The people writing and using this documentation must actually follow this convention for it to have an impact.

# Let's say I'm convinced - how do I get started?

## Get your team on board

If you're working in a development team, pitch this idea to your team, to get buy-in. Most developers I know are frustrated by insufficient and outdated devdocs, so this might be charging at an open door.

## Just do it

This should be fairly easy as well, just decide on a marker symbol, and start writing these documentation comments whenever there's some relevant information for understanding the code that can't be expressed in the code itself.

# Is there any tooling for this?

I am currently in the process of building it. ;-)

It is called [hyperlit](https://github.com/manuel-woelker/hyperlit) - if you're interested, drop by and let me know your thoughts!

*Full disclosure:* \
I had Claude Code review this post before publishing. The text was all written by an organic neural network (i.e. me). All errors and omissions are entirely my own.