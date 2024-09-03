---
layout: page
title: Debugging
permalink: /policies/debugging/
parent: Policies
nav_order: 2
---

## Debugging
One of the objectives of this class is to provide students with experiences writing new code for large, existing codebases.
We anticipate that you may run into difficulties debugging the project code: it is often difficult to build debugging skills until you have a problem in front of you that requires them.
The course staff is happy to help you with debugging, with the specific goal of helping you learn to successfully apply *scientific debugging*.

Andreas Zeller's *Debugging Book* provides an excellent [guide to scientific debugging](https://www.debuggingbook.org/html/Intro_Debugging.html#The-Scientific-Method).
The short version is roughly: if you can't debug an issue in the first few minutes "just by looking at it", it will be hard to keep all of the relevant information in your head at once, and a formal process to help you generate and refine guesses for *why* something is wrong can be immensely useful.

The key idea is to create a debugging note file, where you track information like:
1. What was the input/application state that caused the bug?
1. What was the behavior that I expected?
1. What was the behavior that I observed?
1. What are possible hypotheses for that behavior?
1. How have I tested those hypotheses, and what was the result?

The overall goal with hypothesis formulation is to come up with possible causes for why the bug exists.
Then, as long as those hypotheses are testable, we can prove or disprove them. 
Most hypotheses will be along the lines of "did I make an incorrect assumption about how a library or API works."
The devil is in enumerating all of the possible incorrect assumptions that you might have made, and testing them.
The best way to attack these kinds of problems is to start with testing some high-level, general assumptions, and then refine them. 

If you come to us for debugging help, we will ask you to answer these 5 questions, as our goal is to help you *get better at debugging* and not to simply point out bugs that we might have seen before.
We are happy to discuss the problematic behavior that you are observing, possible hypotheses for why that behavior is occurring, and strategies to test those hypotheses.
In the past, students have found that using a variety of strategies to test their hypotheses (e.g. using a debugger, creating a minimized test case, measured application of `console.log` statements, internet research) are useful, and we would be happy to demonstrate these.
We may not be able to stay with you while you work on refining your hypotheses and fixing the bug, but would be happy to continue following up if you get stuck again.

