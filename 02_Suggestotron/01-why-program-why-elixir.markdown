---
layout: page
title: Why program? Why elixir?
date: 2016-08-04 23:08:17 -0700
position: 1
---

## Why Elixir?
  Right at the start, Elixir is fast. It runs as well as or better than any other language at its level of abstraction, that is how far away from machine code it is. It's designed to work with modern computers that have many CPU cores that run in parallel, and even across networks. It has a pretty easy to understand syntax, relative to some languages. The official docs are thorough, with examples of how to use the functions and modules that are included in the language. It's relatively young, and the community is very welcoming to new people.
  
## Why Functional Programming?
  
  At their lowest level, computer programs are a step-by-step series of instructions to follow.

  As you can imagine, programs written this way can be difficult to understand. Over time, a diverse variety of computer languages were created. These languages allow programmers to write programs at a higher level - the program can later be translated to the lower level instructions.
  Think about a car. When you're driving, you might like to accelerate - but rather than having to know the details of how exactly the car does it, you can press down on the gas pedal.
  Computer programs can be much more complicated than a car. Programming languages give us important tools (called abstractions) that we can use to create them without getting overwhelmed by all the lower level details.
  In this course, we’re going to use Elixir, which is a functional programming language. Functional programming’s primary construct is (surprise!) a function, much like you might remember from algebra class.
  `f(x) = 2x + 1`
  
  Functions in your Elixir program really aren’t that much different.
  
  ```
      def f(x) do
        2 * x + 1
      end
  ```    
  
  An Elixir program is made up of many such functions, chained together. We can visualize each function as a step in a pipeline, transforming an initial value multiple times until a final result is computed. 
  The goal of the functional approach is to construct a complicated program out of small, easy to understand pieces. Individual functions can be “referentially transparent”, a fancy way of saying that they always produce the same value, given the same input. Functions can be composed together easily, passing the output of one to the input of another, creating bigger functions that do more complicated things. By following this approach, we’ll be able to build an entire web application. 
  
