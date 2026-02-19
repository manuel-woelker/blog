---
title: "Let's Write Developer Documentation Driven by Questions"
date: 2026-02-19T06:10:44+01:00
draft: false
tags: ["documentation"]
categories: []
description: "Hypothesis: Using questions to drive and shape documentation makes it easier to read and write."
author: "Manuel Woelker"
showToc: true
---

## How can we improve developer documentation?

More thoughts on improving the documentation process and experience:

A core issue with documentation is that it **does not answer the right questions**.
Oftentimes, there is documentation, but it only rehashes the code, without adding any value, or describes some irrelevant aspect.

My hypothesis is that by applying **Question-Driven Documentation (QDD)**, i.e using **questions as headings**, and letting them drive the documentation 
process, we can improve the quality of the 
documentation.

## What does this look like in practice?

Observant readers might have noticed that this post uses questions as headings, i.e. applying this principle.

The idea is to **start with these questions as headings and then answer them in the following paragraph**.

There is quite a bit of precedent for this approach, e.g. How-Tos, Frequently Asked Questions (FAQs), Q&As,
or even the [Socratic Method](https://en.wikipedia.org/wiki/Socratic_method).

Stack Overflow was basically an entire *site* centered around this idea.

Here are some concrete examples:

| Conventional    | Question Driven                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| Introduction    | What does this do for me?                                                                           |
| Architecture    | What are the components of this system?  <br/> How do they interact?  <br/>What are the interfaces? |
| Recommendations | What should be done? <br/>What are the next steps?                                                  |
| Tutorial        | How do I get started? <br/>What do I need to get started?                                           |
| Security        | How is this made secure? <br/>What are the considered attack vectors?                               |
| Metrics         | What metrics are required? <br/>How are they gathered, processed and reported?                      |
| Performance     | What are the performance objectives? <br/>How are they achieved?                                    |


## What are the benefits of this approach?

I have been experimenting quite a bit with this approach and I have found the following benefits:

1. **Easier to write**: Writing good documentation is hard. By using questions as the drivers for the documentation, I find it easier to focus on answering 
   just one aspect. If this leads to new questions, I can just add them and continue writing.

2. **Easier to read**: As a reader, I also find the question-based structure easier to parse. It also helps set expectations: As a reader I have a better 
   understanding of what to expect from the documentation, much better than with generic headings like "Architecture", "Security"

3. **Focus on the relevant bits**: This question-driven approach puts emphasis on the important questions, rather than describing everything in middling 
   detail.

## What are some good questions to ask?

Here are some question patterns that I found useful:

1. **How do I use this/apply this/... ?**: When writing developer documentation, the proper (or at least intended) use is a great place to start.
2. **Why is it done this way?**: The code often describes the *how*, but documenting the *why* is really important for understanding.
3. **Why is it *not* done this other way?**: Counterfactuals (i.e. things that are not there) are often overlooked, but it may be equally important to 
   communicate, why things are not done in a certain way (e.g. for legal, performance, security reasons, etc.)
4. **What assumptions does this code/architecture make?**: Not all assumptions or preconditions can be expressed in code. But it is often vital for 
   understanding to make these explicit.

## What are the drawbacks of this approach?

The drawbacks as far as I can see are:

1. **It is not a silver bullet**: This won't magically fix our documentation, it is just another step to make it a little better.
2. **Questions take longer to parse**: Questions are longer to read than simple headings, which might slow down the reader.
3. **Unfamiliarity**: This style might feel weird to some readers (and authors) and take some getting used to.
4. **Not universally applicable**: Not all documentation might be suitable for this approach, so judgement should be used when applying it.

## How do I get started?

1. **Discuss it with your team**: First you'll want to get buy-in from your team.
2. **Document this**: (How very meta) Might be a good idea to add a section to your documentation titled "How do we document our code?"
3. **Live it**: Start writing documentation this way.

## What are some patterns to put this into practice?

Here are some heuristics that might help get you started:

1. Whenever there's a question in your Slack channel or team chat of choice, consider adding this question (and answer of course) to your documentation.
2. If you have questions while reading code, just add it, leaving the body as "TODO", and find someone to answer them. A variant of this might be to 
   apply 
   [Cunningham's Law](https://en.wikipedia.org/wiki/Ward_Cunningham#%22Cunningham's_Law%22): *"The best way to get the right answer on the Internet is not to ask a question; it's to post the wrong 
   answer."*
3. To generate questions, start with the basic question of "What do I need to know to understand this?" 

*Full disclosure:* \
I had Codex review this post before publishing. The text was all written by an organic neural network (i.e. me). All errors and omissions are entirely my own.