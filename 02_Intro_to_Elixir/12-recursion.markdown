---
layout: page
title: Recursion
date: 2016-10-1 13:38:30 -0700
---

## Recursion

In elixir, we don't have the concept of loops, which in other languages allow us to iterate over a set of values. Instead, we have the concept of recursion.

Let's look at how we would iterate over a list. We want to start by grabbing the first item:

```elixir
defmodule Recursion do
  def each(x) do
    [h|t] = x
  end
end
```

Then, we want to call the function with the current item:

```elixir
defmodule Recursion do
  def each(x) do
    [h|t] = x
    function.(h)
  end
end
```

Finally, we call each with the tail of the list, which is everything we haven't operated on yet:

```elixir
defmodule Recursion do
  def each([]), do: nil
  def each(x) do
    [h|t] = x
    function.(h)
    each.(t, function)
  end
end
```

We also define the case where the list is empty, so we don't call `each` infinitely.

For instance, let's say we have a function where we want to implement the [Fibonacci](https://en.wikipedia.org/wiki/Fibonacci_number) sequence in elixir. Fibonacci starts with "1,1" and then adds the previous two numbers to get the next one in the sequence. The simplest way for handling fibonacci functions is to use recursion:

```elixir
defmodule Math do
  def fibonacci(x) when x <= 1, do: x
  def fibonacci(x), do: fibonacci(x - 1) + fibonacci(x - 2)
end
```

Although this might look complex from the outset, it's a fairly succinct method for defining such a complex algorithm.

Erlang (and elixir) implement recursive functions efficiently, so we can rely on recursive statements as a safe, fast method for dealing with recursive functions.
