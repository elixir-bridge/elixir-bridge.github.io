---
layout: page
title: Learning Elixir
date: 2016-08-28 13:38:30 -0700
---

## Goals

By the end of this section, you'll know:

* The basics of Elixir
* Use the elixir REPL to run elixir code
* Run elixir code from a script
* How to find elixir documentation

## Getting started


#### iex

We can use the REPL (Read-Eval-Print Loop) command-line tool to write and run simple elixir calculations directly from the command-line. The REPL tool is great for writing simple elixir code, checking on syntax, and understanding how the Elixir run-time works.

Let's open the Interactive Elixir REPL.

Type `iex` into your command line.


The `iex` command (_I_nteractive _E_li_X_ir), which launches the Interactive EliXir command prompt.

```elixir
>$ iex
Erlang/OTP 19 [erts-8.3] [source] [64-bit] [smp:8:8] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Interactive Elixir (1.4.5) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

From this console, we'll be able to play around and experiment with Elixir. Anytime that you see code prepended by the string `iex> `, this means we're working inside the REPL. Feel free to try it along with us as we go. It's a good way to get your fingers working through writing Elixir.

### h command

The `h` command is the help command. It is very useful to find information the elixir language

Type `h` into the command line

You should see something similar to the following:

```elixir
iex(1)> h
warning: variable "h" does not exist and is being expanded to "h()", please use parentheses to remove the ambiguity or change the variable name
  iex:1


                                  IEx.Helpers

Welcome to Interactive Elixir. You are currently seeing the documentation for
the module IEx.Helpers which provides many helpers to make Elixir's shell more
joyful to work with.

This message was triggered by invoking the helper h(), usually referred to as
h/0 (since it expects 0 arguments).

You can use the h/1 function to invoke the documentation for any Elixir module
or function:

    iex> h Enum
    iex> h Enum.map
    iex> h Enum.reverse/1

You can also use the i/1 function to introspect any value you have in the
shell:

    iex> i "hello"

There are many other helpers available:
```

### Notation

In this section, we'll be using a few notations it's good to know about before we start.

If you see the notation of of a name followed by a `/` and number, this indicates a function and it's number of arguments (arity).

* `is_integer/1` - indicates a function called `is_integer` that accepts `1` argument

Newer versions of IEx have implemented the h/1 command. 'h' is a quick access to the docs. Let's try it with the `Integer.to_string`:

Type: `h Integer.to_string` into command line

```elixir
iex(4)> h Integer.to_string

                             def to_string(integer)

Returns a binary which corresponds to the text representation of integer.

Inlined by the compiler.

## Examples

    iex> Integer.to_string(123)
    "123"

    iex> Integer.to_string(+456)
    "456"

    iex> Integer.to_string(-789)
    "-789"

    iex> Integer.to_string(0123)
    "123"
```

* So as you can see, the `h` method shows you the arguments the function takes and examples of how it is used.
In this case `Integer.to_string` takes an integer and returns a string.

* There is a second function defined by Integer.to_string defined in the docs. But we won't worry about that for now.

To exit the `iex` prompt, press `Ctrl+c` twice.

## Official documentation

It's always a great idea to be able to look through documentation when you have a question. Using documentation is often overlooked as a skill and thus, we propose it's a great idea to start with documentation from the beginning.

The official documentation can be found on the [elixir docs](http://elixir-lang.org/docs.html) page. We'll be using the latest _stable_ version of the docs, which can be found on the elixir docs page above and is also available at [http://elixir-lang.org/docs/stable/elixir/Kernel.html](http://elixir-lang.org/docs/stable/elixir/Kernel.html).


## Loading Files

There are several different ways to load files into our interactive shell. Using the `c` command we can tell our REPL which file to compile.

Let's create a file names 'calc.ex'

type the following into the command line:

```bash
touch calc.ex
```

```elixir
c("calc.ex")
```

using the `r` command we can recompile.

```elixir
r (Calc)
```

To see what the `r` function does we can use our help command

Type: `h r` into the terminal

```elixir
iex(1)> h r

def r(module)

Recompiles and reloads the given module.

Please note that all the modules defined in the same file as module are
recompiled and reloaded.

This function is meant to be used for development and debugging purposes. Do
not depend on it in production code.
```

### Arity

We have mentiond the term Arity a few times. Arity means the number of arguments a function takes.

In Elixir when we see a function name it will include the `arity` of the function

```elixir
rem/2
c/1
```

We can see that the `rem` function has an arity of 2.

The `c` or compile function has an arity of 1.
