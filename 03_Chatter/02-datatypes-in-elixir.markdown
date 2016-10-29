---
layout: page
title: Learning Elixir
date: 2016-10-29 13:38:30 -0700
---

## Goals

By the end of this section, you'll know:

* The basics of Elixir
* Use the elixir REPL to run elixir code
* Run elixir code from a script

We can use the REPL (Read-Eval-Print Loop) command-line tool to write and run simple elixir calculations directly from the command-line. The REPL tool is great for writing simple elixir code, checking on syntax, and understanding how the Elixir run-time works.

Before we move on any further, let's open the Interactive EliXir REPL. After installing Elixir, we'll have at least three new commands. One of these commands is the `iex` command (_I_nteractive _E_li_X_ir), which launches the Interactive EliXir command prompt.

![eix prompt](/assets/learning_elixir/iex-cli.png)

From this console, we'll be able to play around and experiment with Elixir. Anytime that you see code prepended by the string `iex> `, this means we're working inside the REPL. Feel free to try it along with us as we go. It's a good way to get your fingers working through writing Elixir.


To exit the `iex` prompt, press `Ctrl+c` twice.


### Notation

In this section, we'll be using a few notations it's good to know about before we start.

If you see the notation of of a name followed by a `/` and number, this indicates a function and it's number of arguments (arity).

* `is_integer/1` - indicates a function called `is_integer` that accepts `1` argument

## Official documentation

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

We'll use all of these types throughout this course.



## Number

A number type comprises the Integer and the Float types. Just like how it sounds, the number types are plain ole' numbers.


### Integer

In our `eix` command prompt, these are all integers:

```elixir
iex> 1
iex> 200000
iex> 0xA
iex> 0b011
iex> 0x11
```

> [Docs for Integer](http://elixir-lang.org/docs/stable/elixir/Integer.html)

Notice that we can create not only base-10 numbers, but octal, hex, and even binary numbers with elixir and it understands both.

We can check if a value is an integer by using the function `is_integer/1`. For instance:

```elixir
iex> is_integer(1) # true
iex> is_integer(3.14) # false
```

### Floats

Creating/using floats is equally as easy. The difference between a float and an integer is indicated by it's precision. They require a dot followed by at _least_ one digit. These are all floats:

```elixir
iex> 1.0
iex> 2000.8
iex> 1.0e-10
```

We can check if a value is a float by using the `is_float/1` function.

The built-in number types have functions we can perform on them as well, such as addition, division, mixing precision, and more.

```elixir
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

```elixir
iex> is_integer(1 + 1) # true
iex> is_float(div(10, 2)) # false
iex> is_boolean(10 / 2) # false
iex> is_boolean(10 / 2 == 5) # true
```
It's possible to check if a variable is a boolean by using the `is_boolean/1` function:

```elixir
iex> is_boolean(true) # true
iex> is_boolean(1) # false
```

## Strings

Strings in Elixir are similar to other languages which are values between _double quotes_ (`"`) and are UTF-8 encoded. For instance, these are all strings:

```elixir
iex> "hello world"
iex> "hello\nworld\n"
```

We can print strings by using the `IO` module. The IO module is the main mechanism in Elixir for reading and writing to standard input/output (:stdio), standard error (:stderr), files and other IO devices. It is pretty straightforward to use.
 
 We can print a string by using the `IO.puts/1` command.
 
```elixir
iex> IO.puts "hello world"
hello world
:ok
iex> IO.gets "yes or no? "
yes or no? yes
"yes\n"
```


We'll come back to using `IO.puts/1` when we write to files which we'll run.

Just like integers, the `String` module has a lot of functions built-in to the standard library we can use out of the box.

```elixir
iex> String.length("hello world") # 11
iex> String.upcase("hello world") # HELLO WORLD
```  

We can concatenate strings using the `<>` operator.

```elixir
iex> "Hello" <> "World" # "HelloWorld"
```

More documentation on the [String](http://elixir-lang.org/docs/stable/elixir/String.html) module is available at [http://elixir-lang.org/docs/stable/elixir/String.html](http://elixir-lang.org/docs/stable/elixir/String.html).


## Functions

In elixir a function is defined by its name and its arity

```elixir
def sum, do: 0
def sum(a), do: a
def sum(a, b), do: a + b
def sum(a, b, c), do: a + b + c

sum 1, 2
#=> 3

sum [1], [2]
#=> [1, 2]

sum "a", "b"
#=> "ab"
```

## Anonymous Functions




## Atoms

We'll use atoms a lot in Elixir. They are their own constant values. If you're familiar with Ruby, these are symbols.

For instance, these are all atoms:

```elixir
iex> :hello
iex> :world
iex> true
```

Atoms have their own value in Elixir. We've actually already seen an atomic value in the booleans. Booleans are actually atoms themselves. We can check if a particular value is an atom by using the `is_atom/1` function:

```elixir
iex> is_atom(:hello) # true
iex> is_atom(2.0) # false
iex> is_atom(true) # true
