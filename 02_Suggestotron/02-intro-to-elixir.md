---
layout: page
title: Intro to Elixir
date: 2016-10-01 13:38:30 -0700
---

## Goals

By the end of this section, you'll know:

* Be able to use the basic building blocks of Elixir code
* Use IEX to run Elixir code
* Do simple calculations
* Use and understand variables
* Use and understand arrays
* Use loops and conditional statements

## Step 1

Type this in the terminal to start the Interactive Elixir shell, a program which lets you try out Elixir code:

```bash
$> iex
```

Yours might look different, but it should look something like this:

```elixir
Interactive Elixir (1.3.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

## Step 2

Next try some simple math that's built into Elixir. Type these lines into IEX:

```elixir
iex> 3 + 3
iex> 7 * 6
```
## Step 3

**Variables** are names with values assigned to them.

```elixir
iex> my_variable = 5
```

This assigns the value `5` to the name `my_variable`.

## Step 4

You can also do math with variables:

```elixir
iex> my_variable + 2
iex> my_variable * 3
```

## Step 5
Variables can also hold more than one value. This is called an **array**.

```elixir
iex> fruits = ["kiwi", "strawberry", "plum"]
```

Here we're using the variable `fruits` to hold a collection of fruit names.

## Step 6

```elixir
iex> fruits ++ ["orange"]
iex> fruits -- ["kiwi"]
```

`++` and `--` are called operators. We can use them with the list of fruits similar to how we can use them with numbers.

## Step 7

Everything in Elixir has a **type**. Type this into IEX:

```elixir
iex> is_number(7)
iex> is_string("kiwi")
iex> is_list(fruits)
```

These are the three data types introduced so far: **Number** (numbers), **String** (text), and **List** (lists).

## Step 8

Each type has different **methods** that can be used on **values** of that type.

```elixir
iex> List.first(fruits)
iex> String.reverse("Hello, world!")
iex> String.upcase("Hello, world!")
```

You can **pipe** method calls together:

```elixir
iex> "Hello, world!" |> String.upcase |> String.reverse
```

## Step 9

Arrays have a method called **each** which iterates through the list running code on each item.

```elixir
Enum.each fruits, fn(fruit) ->
  IO.puts fruit
end
```

This takes the first item from the `fruits` array (`\"strawberry\"`), assigns it to the variable `fruit`, and runs the code between `->` and `end`. Then it does the same thing for each other item in the list. The code above should print a list of the fruits.

## Step 10

A **conditional** runs code only when a statement evaluates to true.

```elixir
if my_variable > 1 do
  IO.puts "YAY!"
end
```

This prints `YAY!` if the value stored in `my_variable` is greater than 1.

Try changing the `>` in the conditional to a `<`.

If you want to do something else when the statement evaluates to false, you can use an `else`:

```elixir
if my_variable > 1 do
  IO.puts "YAY!"
else
  IO.puts "BOO!"
end
```

## Step 11

You can also make your own methods:

```elixir
pluralize = fn(word) ->
  word <> "s"
end
pluralize.("kiwi")
```

Methods take **parameters**, which are the variables they work on. In this case, we made a method called pluralize that takes one parameter, a word.

Methods can also return data. In this case, pluralize returns the word with an 's' added to the end of it. In Elixir, methods return whatever the last line of the method evaluates to.

## Step 12

Putting it all together, let's make a method that says your opinion of some fruits:

**Don't try to type this all in!** Just paste it into iex and see what happens.

```elixir
my_opinion = fn(fruits) ->
  Enum.each fruits, fn(fruit) ->
    if fruit == "pizza" do
      IO.puts "pizza is the best!!!"
    else
      IO.puts pluralize.(fruit) <> " are pretty good, I guess..."
    end
  end
end
my_opinion.(["apple", "pizza", "orange"])
```

Try changing this method to say what your favorite fruit is.

Before you move on to the next step you must exit IEX by pressing 'Control+C' twice.
