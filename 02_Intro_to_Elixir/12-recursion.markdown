---
layout: page
title: Recursion
date: 2016-10-1 13:38:30 -0700
---

## Recursion

Since data is immutable, we don't have traditional loops, like the `for` loop, that you might be familiar with from imperative languages. Instead, we have recursion where a function is called recursively until a condition is reached that stops that action from continuing.

Let's look at how we would iterate over a list. We want to start by grabbing the first item:

```elixir
defmodule Recursion do
  def each(x) do
    [ head | tail ] = x
  end
end
```

Then, we want to call the function with the current item:

```elixir
defmodule Recursion do
  def each(x) do
    [ head | tail ] = x
    function.(head)
  end
end
```

Finally, we call `each` with the tail of the list, which is everything we haven't operated on yet:

```elixir
defmodule Recursion do
  def each([]), do: nil
  def each(x) do
    [ head | tail ] = x
    function.(head)
    each.(tail, function)
  end
end
```

We also define the case where the list is empty, so we don't call `each` infinitely.

For instance, let's say we have a function where we want to implement the [Fibonacci](https://en.wikipedia.org/wiki/Fibonacci_number) sequence. Fibonacci starts with "1,1" and then adds the previous two numbers to get the next one in the sequence. The simplest way for handling fibonacci functions is to use recursion:

```elixir
defmodule Math do
  def fibonacci(x) when x <= 1, do: x
  def fibonacci(x), do: fibonacci(x - 1) + fibonacci(x - 2)
end
```

Although this might look complex from the outset, it's a fairly succinct method for defining such a complex algorithm.

Elixir implements recursive functions efficiently so we can rely on recursive statements as a safe and reliable solution. They are an important part of the language so knowing how it works is helpful but you'll rarely use recursion to manipulate lists. The `Enum` module already provides many of the conveniences for working with lists. We'll use `Enum` a bit in the Phoenix class.
