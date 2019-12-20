---
title: "A Different Semester"
date: 2019-11-28T18:28:05+08:00
author: 'Julius Putra Tanu Setiaji'
---

My 5th semester in NUS is different from my previous semesters.
For one, I no longer stay in Tembusu College, but instead in this godforsaken place called PGP.
I can rant on and on about how PGP is so much worse compared to the Tembusu College or any other Residential College at UTown (University Town), but that's not really the focus of this post.
Instead, this semester also marks my first time of taking purely Computer Science (CS) mods.

Some of you might be aware that I am taking CS3216 this semester, with a long title that basically boils down to "Product Development/Engineering".
It is worth 5 MC, which like any other 5MC modules in the NUS School of Computing (SoC), actually is a lie.
A 5 MC module tends to have higher workload than 8MC modules even.
Luckily, I had been overloading in my earlier semesters, so this semester I can afford to underload below the normal workload of 20 MC (or technically 18 MC according to University regulations).
Although I ended up just taking 4 modules for 17 MCs, originally I took 7 modules.
I will go through each of them below, you can take this as a kind of module review too I guess?

Another thing that I note for this semester is that I wrote so many lines of code in so many languages.
All in all, I wrote about 11 languages for both school and non-school related projects.
I'll go into more details after this listing:
- **Erlang**: One of my proudest achievements this semester is that I made a non-trivial contribution to the Erlang/OTP standard library!
- **C**: Because BIFs in Erlang are written in C. Also, as a TA for CS3210 Parallel Computing, I had to write some skeleton code in C for the assignments.
- **Elixir**: For all my CS3216 web backends, because Elixir is so good <3
- **TypeScript/JavaScript**: For all the CS3216 frontends. I was pleasantly surprised by how nice TypeScript is.
- **Scala**: I used this for CS4223 Multicore Architecture because we can choose to write in whatever language that we want.
- **Haskell**: The main language used in CS2104 Programming Language Concepts
- **Prolog**: Also taught in CS2104
- **OCaml**: Aaaand also taught in CS2104
- **LaTeX**: As with every semester, I wrote all my cheatsheet in LaTeX. But additionally this semester I initiated a new series of events organised by NUS Hackers called Hacker Tools, where I taught a session on LaTeX.
- **Shell**: I used this as a kind of glue code when fuzzy testing my CS4223 assignments among other things.
- **Python**: I used this for CS3243 Introduction to AI, simply because the mod requires that.
- **Ruby**: Whenever I have to write quick scripts, like parsing the results of the fuzzy testing in CS4223.

# Erlang/OTP -- Fix `file:allocate/3` "broken" behaviour
You can find more context at the following links:
- https://github.com/erlang/otp/pull/2386 and https://bugs.erlang.org/browse/ERL-1042
- https://github.com/erlang/otp/pull/2408 and https://bugs.erlang.org/browse/ERL-1056

# Hacker Tools
Modelled after https://missing.csail.mit.edu/

You can find my slides at https://github.com/indocomsoft/hackertools-slides

# CS3216: https://pinda.fun
NUS School of Computing's Product Development course, where my team managed to win the Category Winner.

It's written in TypeScript using the React Framework, and Elixir using the Phoenix Framework.

Read the source code at https://github.com/pinda-fun/pinda-fun/

# CS4223: Tracing Simulator for MESI, MOESI, Dragon Cache Coherency Protocols
Written in Scala, using the bazel build system.

Read the source code at https://github.com/indocomsoft/cs4223-assignment-2

# CS3243 Introduction to AI Assignments
Written in Python, where I optimised the code using cProfile to get the bonus marks for performance.

It's their fault to choose such a language as Python where using the wrong constructs can lead to slowdowns in your programme.

Read the source code at the following links:
- https://github.com/indocomsoft/cs3243-assignment-1
- https://github.com/indocomsoft/cs3243-assignment-2
- https://github.com/indocomsoft/cs3243-assignment-3

# CS2104: Prolog Parser and Interpreter
It was really annoying because we are given a useless lexer, but I guess I managed to implement a Prolog interpreter that supports the cut operator in Haskell.

Read the source code at https://github.com/indocomsoft/cs2104-lab4
