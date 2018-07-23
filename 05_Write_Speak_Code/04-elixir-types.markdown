---
layout: page
title: Elixir Types
date: 2016-08-28 13:38:30 -0700
---

## Goals

By the end of this section, you'll know:

* Gain an understanding of basic Elixir Types

## Types

Although Elixir is not a statically typed language, it does have the concept of types. The basic types we'll work with are:

* Numbers
* Floats
* Booleans
* Strings
* Atoms
* Lists
* Tuples

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
Basic math operations like the one above work as you would expect them to (Subtraction, Multiplication etc.)

We can check if a value is an integer by using the function `is_integer/1`. Try it! Type `is_integer(42)` into IEx, and press enter. You should see something like the following:

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

> [Docs for Integer](http://elixir-lang.org/docs/stable/elixir/Integer.html)

### Floats

Creating/using floats is the same as creating integers, typed as you might expect: They require a dot followed by at least one digit. Try typing the following floats in IEX:
```elixir
iex> 1.0
iex> 2000.8
iex> 1.0e-10
```

We can check if a value is a float by using the `is_float/1` function.
Type the following into iex:

```
iex> is_float(3.14)
true
```

Let's see what other mathematical operations we can practice.

Try typing some of the operations listed bellow into your iex console.

```elixir
iex> 1 + 1        # 2
iex> div(10, 2)   # 5
iex> rem(10, 3)   # 1
iex> ## Or without parenthesis
iex> rem 10, 3    # 1
iex> 10 / 2
```

As you can see operations we are familiar with like `div/2` behave as we expect

```
iex> div(9, 3)
3
```

What about operators that look less familiar?

The `rem` operator will return the remainder of a division operations

```
iex> div(10, 3)
1
```

Try some other commands out to see what else you can do.

> [Float docs](http://elixir-lang.org/docs/stable/elixir/Float.html)


### Hex, Octal, Binary

Elixir supports notations for entering binary, hex, octal, and hexadecimal numbers

```Elixir
0b0010
0x644
0x1F
```

But let's not worry about these for now.

### Boolean

Booleans are `true` and `false` types. We can use these types to check truth conditions.

Type the following lines(one at a time) into the iex console:

```elixir
iex> true ## true
iex> true == false
```

It's possible to check if a variable is a boolean by using the `is_boolean/1` function:

Try typing the following into the console:

```elixir
iex> a = 1
iex> is_boolean(true) # true
iex> is_boolean(a) # false
iex> false
iex> true
```

Elixir also provides `or`, `and`, `not` as boolean operators. These operators are strict in that they expect a boolean as an argument.

Type the following into the console:

```elixir
42 && true
nil || 42
```

## Strings

Strings in Elixir are values between _double quotes_ (`"`) and are UTF-8 encoded. Try typing the following one line at a time into the console (feel free to copy and paste the last one):

```elixir
iex> "Hello"
iex> "World"
iex> "❤️💛💚💙"
```

We can output values to the console using the `IO.puts/1` command. Let's try and output our string to the console. Type the following:

```
iex> IO.puts("hello world!")
hello world!
:ok
```

It prints the string to stdout by default, and then returns the `:ok` tuple, to indicate that there were no errors.

Just like integers, the `String` module has a lot of functions built-in to the standard library we can use out of the box.

Type the following lines onto the console one at a time:

```elixir
iex> String.length("hello world") # 11
iex> String.upcase("hello world") # HELLO WORLD
```

#### String Interpolation

type the following into the console

```elixir
receiver = "World"
"Hello #{receiver}"
```

Variables are interpolated using the `#{variable}`


More documentation on the [String](http://elixir-lang.org/docs/stable/elixir/String.html) module is available at [http://elixir-lang.org/docs/stable/elixir/String.html](http://elixir-lang.org/docs/stable/elixir/String.html).

### Concatenate Operator

So what happens when we want to put two separate strings together?

We use the concatenate operator.

It looks like this: `<>`

Now try using it. Type the following into the console:

```elixir
iex> "Hello" <> "World" # "HelloWorld"
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

