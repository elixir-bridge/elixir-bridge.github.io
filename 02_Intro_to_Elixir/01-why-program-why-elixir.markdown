---
layout: page
title: Why program? Why elixir?
date: 2016-08-04 23:08:17 -0700
position: 1
---

## Why Functional Programming?
  In this course, we’re going to use Elixir, which is a functional programming language. Functional programming’s primary construct is (surprise!) a function, much like you might remember from algebra class.
  `f(x) = 2x + 1`

  Functions in your Elixir program really aren’t that much different.

  ```
      def f(x) do
        2 * x + 1
      end
  ```

  An Elixir program is made up of many such functions, chained together. We can visualize each function as a step in a pipeline, transforming an initial value multiple times until a final result is computed.

  The goal of the functional approach is to construct a complicated program out of small, easy to understand pieces. Individual functions can be “referentially transparent”, a fancy way of saying that they always produce the same value, given the same input.

  Functions can be composed together easily, passing the output of one to the input of another, creating bigger functions that do more complicated things. By following this approach, we’ll be able to build an entire web application.


## Why Elixir?

There are several reasons why people are excited about Elixir. Let's take a look at a few below.

#### Scalable

All elixir code runs inside of something called processes (think lots of little programs). Each Program can exist on its own and it communicates with other programs via message passing.

Because each "process" does not take up a lot of processing power, hundreds of thousands of programs could be running at the same time potentially on different computers. Since each `process` is isolated it can be garbage collected independently. This reduces pauses that are system wide. This feature also allows all machine resources to be used as efficiently as possible.

#### Fault-tolerant

Knowing that things will go wrong inside of a program - elixir introduces the concept of supervisors. Supervisors understand how to restart parts of your system when things go wrong - so that entire program does not stop running if part of it happens to break.

#### Functional

Functional programming allows developers to design code that is short, fast, maintainable, and does not have unexpected side effects that might be seen in an imperative language

#### Very Extensible

Elixir has been designed to let developers naturally extend the language to various domains.

#### Built off Erlang

Erlang is a functional programming language that was developed by Ericcson in the 1980's. Given it's maturity, the language and run-time environment are very stable and optimized for efficiency.

#### Telco Strong

Erlang has nine nines reliability. Meaning that any Erlang program will have be up and running 99.9999999% of the time

#### Hot Reload Friendly

As there is a run time available, Elixir allows you to start, stop, load, and unload processes. We can provide code for the runtime to load and replace other code without having to restart our system.

#### Soft real-time

Since real-time features are becoming increasingly important, as the web moves to a more complex, desktop-app-like-feeling, we want to be able to build features that make writing real-time applications less complex. Out of the box, erlang (and therefore Elixir) allows us to build applications to run in almost real time.

### Garbage Collection

* Very fast
* No global lock for garbage collection
* Very efficient
