---
layout: post
title: learning_elixir
date: 2016-08-28 13:38:30 -0700
---

## Goals

By the end of this section, you'll know:

* The basics of Elixir
* Use the elixir REPL to run elixir code
* Run elixir code from a script
* How to find elixir documentation

## Getting started

We can use the REPL (Read-Eval-Print Loop) command-line tool to write and run simple elixir calculations directly from the command-line. The REPL tool is great for writing simple elixir code, checking on syntax, and understanding how the Elixir run-time works.

Before we move on any further, let's open the Interactive EliXir REPL. After installing Elixir, we'll have at least three new commands. One of these commands is the `iex` command (_I_nteractive _E_li_X_ir), which launches the Interactive EliXir command prompt. 

![eix prompt](/assets/learning_elixir/iex.png)

From this console, we'll be able to play around and experiment with Elixir. Anytime that you see code prepended by the string `iex> `, this means we're working inside the REPL. Feel free to try it along with us as we go. It's a good way to get your fingers working through writing Elixir.

### Notation

In this section, we'll be using a few notations it's good to know about before we start. 

If you see the notation of of a name followed by a `/` and number, this indicates a function and it's number of arguments (arity). 

* `is_integer/1` - indicates a function called `is_integer` that accepts `1` argument

## Official documentation

It's always a great idea to be able to look through documentation when you have a question. Using documentation is often overlooked as a skill and thus, we propose it's a great idea to start with documentation from the beginning.

The official documentation can be found on the [elixir docs](http://elixir-lang.org/docs.html) page. We'll be using the latest _stable_ version of the docs, which can be found on the elixir docs page above and is also available at [http://elixir-lang.org/docs/stable/elixir/Kernel.html](http://elixir-lang.org/docs/stable/elixir/Kernel.html). 

## Types

Although Elixir is not a statically typed language, it does have the concept of types. The basic types we'll work with are:

* Numbers
* Booleans
* Atoms
* Strings
* Anonymous functions
* Lists
* Tuples
* Custom types

We'll use all of these types throughout this course (and you'll use them throughout your Elixir career), so let's look at how to create/use each one.

## Number

A number type comprises the Integer and the Float types. Just like how it sounds, the number types are plain ole' numbers. 

### Integer

In our `eix` command prompt, these are all integers:

```
iex> 1
iex> 200000
iex> 0xA
iex> 0b011
iex> 0x11
```

> [Docs for Integer](http://elixir-lang.org/docs/stable/elixir/Integer.html)

Notice that we can create not only base-10 numbers, but octal, hex, and even binary numbers with elixir and it understands both.

We can check if a value is an integer by using the function `is_integer/1`. For instance:

```
iex> is_integer(1) # true
iex> is_integer(3.14) # false
```

### Floats

Creating/using floats is equally as easy. The difference between a float and an integer is indicated by it's precision. They require a dot followed by at _least_ one digit. These are all floats:

```
iex> 1.0
iex> 2000.8
iex> 1.0e-10
```

We can check if a value is a float by using the `is_float/1` function. 

The built-in number types have functions we can perform on them as well, such as addition, division, mixing precision, and more. 

```
iex> 1 + 1 # 2
iex> div(10, 2)
iex> rem(10, 3)
iex> ## Or without parenthesis
iex> rem 10 3
iex> Float.ceil(1.234567, 3) # 1.235
iex> 10 / 2
```

Try some other commands out to see what else you can do. 

> [Float docs](http://elixir-lang.org/docs/stable/elixir/Float.html)

We can also call functions on these results as well. For instance:

```
iex> is_integer(1 + 1) # true
iex> is_float(div(10, 2)) # false
iex> is_boolean(10 / 2) # false
iex> is_boolean(10 / 2 == 5) # true
```

### Boolean

Booleans are `true` and `false` types. We can use these types to check truth conditions. 

```
iex> true ## true
iex> true == false
```

It's possible to check if a variable is a boolean by using the `is_boolean/1` function:

```
iex> is_boolean(true) # true
iex> is_boolean(1) # false
```

## Atoms

We'll use atoms a lot in Elixir. They are their own constant values. If you're familiar with Ruby, these are symbols. 

For instance, these are all atoms:

```
iex> :hello
iex> :world
iex> true
```

Atoms have their own value in Elixir. We've actually already seen an atomic value in the booleans. Booleans are actually atoms themselves. We can check if a particular value is an atom by using the `is_atom/1` function:

```
iex> is_atom(:hello) # true
iex> is_atom(2.0) # false
iex> is_atom(true) # true
```

## Strings

Strings in Elixir are similar to other languages which are values between _double quotes_ (`"`) and are UTF-8 encoded. For instance, these are all strings:

```
iex> "hello world"
iex> "hello\nworld\n"
```

We can print strings by using the `IO` module (which we'll look at in a few) by using the `IO.puts/1` command. We'll come back to using `IO.puts/1` when we write to files which we'll run. 

Just like integers, the `String` module has a lot of functions built-in to the standard library we can use out of the box. 

```
iex> String.length("hello world") # 11
iex> String.upcase("hello world") # HELLO WORLD
```

More documentation on the [String](http://elixir-lang.org/docs/stable/elixir/String.html) module is available at [http://elixir-lang.org/docs/stable/elixir/String.html](http://elixir-lang.org/docs/stable/elixir/String.html).

## Anonymous functions

In Elixir, we can create functions which are treated just like any other type in Elixir. To create a function, we'll use the keywords of `fn` and `end`. 

For instance, all of these are functions in Elixir:

```
iex> add = fn a, b -> a + b end
iex> is_function(add) # true
iex> b = (fn a -> a + 2 end)
```

In order to actually execute our anonymous functions, we'll need to add a suffix of `.` to the end of the function name. For example, to call the `add/2` function, we'll need to type:

```
iex> add.(2 2) # 4
```

## Lists

Lists in Elixir are created by surrounding a list of values with brackets `[`. Lists don't need to contain only one type. They can hold on to multiple different types in the same list. 

For instance, these are all _valid_ lists:

```
iex> [1, 2, 3]
iex> [:hello, "world"]
```

We have a bunch of built-in methods we can use to interact with and manipulate lists in Elixir. 

```
iex> length [1, 2, 3] # 3
iex> [1] ++ [2] # [1, 2]
```

Common functions we'll use whenever we write Elixir code are checking for the head (`hd/1`) and tails of a list (`tl/1`). When we talk about the head of the list, we're looking for the first element of the list. For instance:

```
iex> hd([1, 2, 3]) # 1
```

The tail is everything _but_ the head of the list:

```
iex> tl([1, 2, 3]) # [2, 3]
```

In Elixir, we'll often work with lists an element at a time, so the `hd/1` command will come in handy. 

## Tuples

Tuples in Elixir are used to store elements contiguously in memory, which means we can get elements in the tuple by it's place within the tuple. Before we get too far ahead of oursevles, let's look at how to create a tuple.

Tuples are created by using the curly brackets with elements separated by commas. These are all tuples in Elixir:

```
iex> {:ok, "hello"}
iex> {1, 2, :true}
```

Because these are created and stored in one block in memory, we can use the indicies to indicate which value we want to pull out of a tuple. For instance, we can get the `:ok` value in the first tuple by looking for the first element:

```
iex> elem({:ok, "hello"}, 0) # :ok
```

We can check the size of a tuple using the `tuple_size/1` function:

```
iex> tuple_size({:ok, "hello"}) # 2
```

And we can replace elements in a tuple by using the `put_elem/3` function, which takes the tuple, the argument, and the value:

```
iex> put_elem({:ok, "hello"}, 1, "world")
```

> Note that Erlang (and thus Elixir) create immutable data. That is, the original tuple is not replaced, but a new tuple based upon the first one is created. 
> 
> It turns out that even though it feels like a hinderance, using immutable data makes our software easier to reason about and never need to worry about overwriting variables in memory (thus preventing race conditions) and more.
> 
> Although we don't need to focus on this now, it's a good idea to keep in mind that no variables is manipulated after it's created, but that a new one is created. 

## Operators

Elixir has

## Executing scripts

// TODO: 

