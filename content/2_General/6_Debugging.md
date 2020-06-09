---
slug: /general/debugging
title: Debugging
author: Benjamin Qi, Aaron Chew
order: 6
---

Detecting issues within your program and figuring out how to avoid them in the first place.

<!-- END DESCRIPTION -->

## Style Guide

[Swift](https://codeforces.com/blog/entry/64218)

## Compilation

As mentioned in "Running C++," I use the following to compile and run.

```
co() { g++ -std=c++11 -O2 -o $1 $1.cpp -Wall -Wextra -Wshadow -DLOCAL -Wl,-stack_size -Wl,0xF0000000; }
run() { co $1 && ./$1 & fg; }
```

### Warnings

See [here](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html).

`-Wall -Wextra -Wshadow` 

### Stack Size

According to [this comment](https://codeforces.com/blog/entry/60999?#comment-449312), `-Wl,-stack_size -Wl,0xF0000000` increases the stack size on Mac (otherwise, you might get a runtime error). 

(Documentation?)

### Other

`-fsanitize=undefined -fsanitize=address` 

`-D_GLIBCXX_DEBUG -g`

(someone want to explain these? I don't use)

## Running

According to [StackOverflow](https://stackoverflow.com/a/60516966/5834770) the `& fg` is necessary for getting `zsh` on Mac to display crash messages (such as segmentation fault).

### Measuring Time & Memory Usage

 - [CF Comment](https://codeforces.com/blog/entry/49371?#comment-333749)
 - [time -v on Mac](https://stackoverflow.com/questions/32515381/mac-os-x-usr-bin-time-verbose-flag)

## CppIO Template

Although not feasible if you have to write all code from scratch, I find [this template](https://github.com/bqi343/USACO/blob/master/Implementations/content/contest/CppIO.h) very helpful for simplifying input / output / debug output. Note that `dbg()` only produces debug output when `-DLOCAL` is included as part of the compilation command, so you don't need to comment out those lines before submitting.

[Examples - Debug Output](https://github.com/bqi343/USACO/blob/master/Implementations/content/contest/CppIO_test.cpp)

## Stress Testing

You can use a [simple script](https://github.com/bqi343/USACO/blob/master/Implementations/content/contest/stress.sh) to test two solutions against each other. See Errichto's [video](https://www.youtube.com/watch?v=JXTVOyQpSGM) on testing solutions for more information.

## Using a Debugger

Using a debugger varies from language to language and even IDE to different IDE. For now I will describe the basic operations of a debugger. 

A debugger allows you to pause a code in its execution and see the values as a given point in the debugger. 

To do this, set a "breakpoint" at a certain line of code. When the code runs to that breakpoint, it will pause and you will be able to inspect all the different variables at that certain instance.

There are two more useful and common operations. Once you are at the breakpoint, you may want to see what happens after the current line is executed. This would be the "Step Over" button that will allow you to move to the next line. Say you are at a line with the following code: `dfs(0,-1)`, if you click "step over" the debugger will ignore showing you what happens in this function and go to the next line. If you click "step in," however, you will enter the function and be able to step through that function.

In essense, a debugger is a tool to "trace code" for you. It is not much different from just printing the values out at various points in your program.

Pros of using a debugger: 
 
 - No need to write print statements so you save time
 
 - You can step through the code in real time
 
Cons of using a debugger:
 
 - You cannot see the overall "output" of your program at each stage. For example, if I wanted to see the every single value of `i` in the program, I could not using a debugger.
 
 - Most advanced competitive programmers do not use debuggers; it is quite time inefficient. 