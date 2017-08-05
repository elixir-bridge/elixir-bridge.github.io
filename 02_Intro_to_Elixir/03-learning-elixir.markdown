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

We can use the REPL (Read-Eval-Print Loop) command-line tool to write and run simple elixir calculations directly from the command-line. The REPL tool is great for writing simple elixir code, checking on syntax, and understanding how the Elixir run-time works.

Before we move on any further, let's open the Interactive EliXir REPL. After installing Elixir, we'll have at least three new commands. One of these commands is the `iex` command (_I_nteractive _E_li_X_ir), which launches the Interactive EliXir command prompt.

![eix prompt](/assets/learning_elixir/iex-cli.png)

From this console, we'll be able to play around and experiment with Elixir. Anytime that you see code prepended by the string `iex> `, this means we're working inside the REPL. Feel free to try it along with us as we go. It's a good way to get your fingers working through writing Elixir.

### Notation

In this section, we'll be using a few notations it's good to know about before we start.

If you see the notation of a name followed by a `/` and number, this indicates a function and it's number of arguments (arity). For example:

* `is_integer/1` - indicates a function called `is_integer` that accepts `1` argument.

Newer versions of IEx have implemented the h/1 command. 'h' is a quick access to the docs. Let's try it with the `Integer.to_string`:

```
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

* There is a second function defined by `Integer.to_string` defined in the docs but we won't worry about that for now.

To exit the `iex` prompt, press `Ctrl+c` twice.

## Official documentation

It's always a great idea to be able to look through documentation when you have a question. Using documentation is often overlooked as a skill and thus, we propose it's a great idea to start with documentation from the beginning.

The official documentation can be found on the [elixir-lang docs](http://elixir-lang.org/docs.html) page. We'll be using the latest _stable_ version of the Elixir documenation which is available at [https://hexdocs.pm/elixir/](https://hexdocs.pm/elixir/).

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

Open up your terminal window and type `iex` to open your interactive elixir shell.

Next type the following expression into the shell and them press enter:

```
1 + 1
```

You should see output like this:

```
iex(5)> 1 + 1
2
```
Basic math operations (subtraction, multiplication, etc.) like the one above work as you would expect them to.

We can check if a value is an integer by using the function `is_integer/1`. Let's try it out! Type `is_integer(42)` into IEx, and press enter. You should see something like the following:

```elixir
iex> is_integer(42)
true
```

Now let's try a number with a decimal point. Type `is_integer(3.14)` into IEx, and press enter. The result should be like this:

```
iex> is_integer(3.14)
false
```

Why is this false? Because 3.14 is not in integer, it's a `Float`. Let's take a look at floats.

> [Docs for Integer](https://hexdocs.pm/elixir/Integer.html)

### Floats

Creating floats is the same as creating integers, typed as you might expect: they require a dot followed by at least one digit. Try typing the following floats in IEx:
```elixir
iex> 1.0
iex> 2000.8
iex> 1.0e-10
```

We can check if a value is a float by using the `is_float/1` function.
Type the following into IEx:

```
iex> is_float(3.14)
true
```

Let's see what other mathematical operations we can practice.

Try typing some of the operations listed below into your IEx console.

```elixir
iex> 1 + 1        # 2
iex> div(10, 2)   # 5
iex> rem(10, 3)   # 1
iex> ## Or without parenthesis
iex> rem 10, 3    # 1
iex> 10 / 2
```

As you can see operations we are familiar with like `div/2` behave as we expect:

```
iex> div(9, 3)
3
```

What about operators that look less familiar?

The `rem` operator will return the remainder of a division operation:

```
iex> rem(10, 3)
1
```

Try some other commands out to see what else you can do.

> [Float docs](https://hexdocs.pm/elixir/Float.html)

### Boolean

Booleans are `true` and `false` types. We can use these types to check truth conditions.

Type the following lines (one at a time) into the IEx console:

```elixir
iex> true ## true
iex> true == false
```

It's possible to check if a variable is a boolean by using the `is_boolean/1` function.

Try typing the following into the console:

```elixir
iex> a = 1
iex> is_boolean(true) # true
iex> is_boolean(a) # false
```

## Atoms

We'll use atoms a lot in Elixir. They are their own constant values. If you're familiar with Ruby, these are symbols or enumerations in C/C++.

For instance, these are all atoms:

```elixir
iex> :hello
iex> :world
iex> :true
iex> :this_has_underscores
```

## Strings

Strings in Elixir are values between _double quotes_ (`"`) and are UTF-8 encoded. Try typing the following one line at a time into the console (feel free to copy and paste the last one):

```elixir
iex> "hello world"
iex> "hello\nworld\n"
iex> "❤️💛💚💙"
```

We can output values to the console using the `IO.puts/1` command. Let's try and output our string. Type the following:

```
iex> IO.puts("hello world!")
hello world!
:ok
```

By default, it prints the string to stdout (short for standard output), and then returns the `:ok` tuple to indicate that there were no errors.

Just like integers, the `String` module has a lot of functions built-in to the standard library we can use out of the box.

Type the following lines into the console one at a time:

```elixir
iex> String.length("hello world") # 11
iex> String.upcase("hello world") # HELLO WORLD
```

So what happens when we want to combine two strings together? We use something called the concatenation operator which looks like: `<>`. 

Now try using it. Type the following into the console:

```elixir
iex> "Hello" <> "World" # "HelloWorld"
```

More documentation on the [String](https://hexdocs.pm/elixir/String.html) module is available at [https://hexdocs.pm/elixir/String.html](https://hexdocs.pm/elixir/String.html).
