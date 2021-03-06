---
title: "Notes: The Elements of Computing Systems by Noam Nisan and Shimon Schocken"
author: jcb
date: 2018-04-23
tags: notes, programming, hardware
---

# Contents

----

-  **Completed**
-  *In Progress*
-  Planned

----

- [Chapter 1: Boolean Logic](/projects/tecp/01)
- Chapter 2: Boolean Arithmetic
- Chapter 3: Sequential Logic
- Chapter 4: Machine Language
- Chapter 5: Computer Architecture
- Chapter 6: Assembler
- Chapter 7: Virtual Machine I, Stack Arithmetic
- Chapter 8: Virtual Machine II, Program Control
- Chapter 9: High-Level Language
- Chapter 10: Compiler I: Syntax Analysis
- Chapter 11: Code Generation
- Chapter 12: Operating System
- Chapter 13: Postscript, More Fun to Go

# Nand2Tetris Tools Setup

The Elements of Computing systems has some accompanying tools on the
[Nand2Tetris website](http://www.nand2tetris.org). These tools include:

1.  A Hardware Simulator to test our circuits written in HDL.
2.  A CPUEmulator to test out instructions on the CPU chip we build in Ch. 05.
3.  An Assembler for turning assembly into machine instructions for our CPU.
4.  A Jack Compiler for turning Jack language files into Assembly.
5.  A Virtual Machine Emulator that runs Operating Systems written in Jack.
6.  A text comparer utility program that checks if two files are equal.

These tools are all Java programs with shell script wrappers. The authors
only have setup instructions for Windows and macOS on the Nand2Tetris website,
but running the tools on Linux is totally possible with a little work.

## Setting up the tools on NixOS + Xmonad

I'm running the [NixOS distribution of Linux](http://www.nixos.org) and the
[XMonad window manager](http://www.xmonad.org).
Version numbers:

```
jcb@daphne~> nix-env --version
nix-env (Nix) 2.0

jcb@daphne~> nixos-version
18.03.132021.c18.03.132021.c0c5571ec1a (Impala)

jcb@daphne~> xmonad --version
xmonad 0.13
```

Suprisingly, my choice of window manager ended up being relevant to getting the
tools to work.

**Step 1**: Download the tools from the
[Nand2Tetris website](http://www.nand2tetris.org/software.php).

**Step 2**: Install the Java Runtime Engine.

```
jcb@daphne~> nix-env -iA nixos.jre
```

**Step 3**: Give the shell script wrapper you want to run executable permissions

```
jcb@daphne~> chmod +x ~/nand2tetris/tools/HardwareSimulator.sh
```

The specific path to the file may be different for you.

**Step 4**: Make Java recognize XMonad

Ordinarily, the previous steps should be enough, but apparently Java GUI's need
a little coaxing to actually display under XMonad. I got stuck for a little
while because I would do

```
jcb@daphne~> bash ~/nand2tetris/tools/HardwareSimulator.sh
```
and get only a blank grey screen. This is a [documented issue between
Java and XMonad](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console)

The solution is to add the line

```
export _JAVA_AWT_WM_NONREPARENTING=1
```
to your `.bashrc` file.

Or if you use the`fish` shell like me, add

```
set -x _JAVA_AWT_WM_NONREPARENTING 1
```

to your `.config/fish/config.fish`.

## Caveat

Seems simple, right? Bear in mind that for me **Step 3.5** was "Take a break to
deal with my confusion and crippling self-doubt caused by being unable to
instantly solve the problem." This step gets left out of many technical guides,
but it's a very important step. You and your machine are one unified system. If
you, the programmer, get demoralized and give up, the problem won't get solved!

When this happens I try to keep in mind the following: Every programmer feels
dumb ~~sometimes~~ often. Feeling dumb is being confronted by a problem you
don't know how to solve. A programmer that doesn't feel dumb is a programmer
that is only working on problems they already know how to solve, that is,
a programmer who's not pushing themselves.

I'm mentioning this because one of the temptations of solving technical problems
is to present the clarity of a solution while retroactively sanitizing the
process by which you arrived at the solution. This is very effective at making
other people think you are smart, but it's not honest, and I think it
demoralizes beginners.

The Elements of Computing Systems is a text that I think is incredibly helpful
for a beginner programmers (or any programmer, in fact). It gives you great
conceptual framework for the whole structure of computing, from the heights of
the application to the foundation of physical circuits. It's also a text that
contains many opportunites for getting stuck, confused and demoralized.

I want to make perfectly clear that this is a normal and expected part of the
process of learning about computers. I personally got stuck and gave up on
Chapter 6 twice in two separate read-throughs over the course of the past few
years. Hopefully this third time will be, as they say, the charm.
