---
title: "Let's Write Developer Documentation Driven by Questions"
date: 2026-02-19T06:10:44+01:00
draft: true
tags: ["documentation"]
categories: []
description: "Hypothesis: Using questions to drive and shape documentation makes it easier to read *and* write."
author: "Manuel Woelker"
showToc: true
---

# How can we improve developer documentation?

More thoughts on improving the documentation process and experience:

A core issue with documentation is that it **does not answer the right questions**.
Oftentimes, there is documentation, but it only rehashes the code, without adding any value, or describes some irrelevant aspect.

My hypothesis is that by simply using **questions as headings**, and letting them drive the documentation process we can improve the quality of the documentation.

# What does this look like in practice?

Observant readers might have noticed that this post uses questions as headings, i.e. applying this principle.

The idea is to **start with these questions as headings and then answer them in the following paragraph**.

There is quite a bit of precedent for this approach, e.g. How-Tos, Frequently Asked Questions (FAQs), Q&As, or even the [Socratic Method](https://en.wikipedia.
org/wiki/Socratic_method).

Stack Overflow was basically an entire *site* centered around this idea.

# What are the benefits of this approach?

I have been experimenting quite a bit with this approach and I have found the following benefits:

1. **Easier to write**: Writing good documentation is hard. By using questions as the drivers for the documentation, I find it easier to focus on answering 
   just one aspect. If this leads to new questions, I can just add them and continue writing.

2. **Easier to read**: As a reader, I also find the question based structure easier to parse. It also helps set expectations: As a reader I have a better 
   understanding of what to expect from the documentation, much better than with generic headings like "Architecture", "Security"

3. **Focus on the relevant bits**: This question driven approach puts emphasis on the important questions, rather than describing everything in middling 
   detail.

# What are some good questions to ask?

Here are some question patterns that I found useful:

1. **How do I use this/apply this/... ?**: When writing documentation it for code, the proper or intended use is a great to document.
2. **Why is it done this way?**: The code often describes the *how*, but documenting the *why* is really important for understanding.
3. **Why is it *not* done this other way?**: Counterfactuals (i.e things that are not there) are often overlooked, but it may be equally important to 
   communicate, why things are not done in a certain way (e.g. for legal, performance, security reasons, etc.)
4. **What assumptions does this code/architecture make?**: Not all assumptions or preconditions can be made expressed in code. But it is often vital for 
   understanding to make these explicit.

# What are the drawbacks of this approach?

The drawbacks as far as I can see are:

1. **It is not a silver bullet**: This won't magically fix our documentation, it is just another step to make it a little better.
2. **Questions take longer to parse**: Questions are longer to read than simple headings, which might slow down the reader.
3. **Unfamiliarity**: This style might feel weird to some readers (and authors) and take some getting used to.
4. **Not universally applicable**: Not all documentation might be suitable for this approach, so judgement should be used when applying it.
