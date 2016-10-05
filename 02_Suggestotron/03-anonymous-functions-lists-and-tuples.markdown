---
layout: page
title: Anonymous Functions Lists and Tuples
date: 2016-10-1 13:38:30 -0700
---

Anonymous functions

In Elixir, we can create functions which are treated just like any other type in Elixir. To create a function, we'll use the keywords of `fn` and `end`.

For instance, all of these are functions in Elixir:

```elixir
iex> add = fn a, b -> a + b end
iex> is_function(add) # true
iex> b = (fn a -> a + 2 end)
```

In order to actually execute our anonymous functions, we'll need to add a suffix of `.` to the end of the function name. For example, to call the `add/2` function, we'll need to type:

```elixir
iex> add.(2 2) # 4
```

## Lists

Lists in Elixir are created by surrounding a list of values with brackets `[`. Lists don't need to contain only one type. They can hold on to multiple different types in the same list.

For instance, these are all _valid_ lists:

```elixir
iex> [1, 2, 3]
iex> [:hello, "world"]
```

We have a bunch of built-in methods we can use to interact with and manipulate lists in Elixir.

```elixir
iex> length [1, 2, 3] # 3
iex> [1] ++ [2] # [1, 2]
iex> [1, 2, 3] -- [2] # [1, 3]
```

Common functions we'll use whenever we write Elixir code are checking for the head (`hd/1`) and tails of a list (`tl/1`). When we talk about the head of the list, we're looking for the first element of the list. For instance:

```elixir
iex> hd([1, 2, 3]) # 1
```

The tail is everything _but_ the head of the list:

```elixir
iex> tl([1, 2, 3]) # [2, 3]
```

In Elixir, we'll often work with lists an element at a time, so the `hd/1` command will come in handy.

## Tuples

Tuples in Elixir are used to store elements contiguously in memory, which means we can get elements in the tuple by it's place within the tuple. Before we get too far ahead of oursevles, let's look at how to create a tuple.

Tuples are created by using the curly brackets with elements separated by commas. These are all tuples in Elixir:

```elixir
iex> {:ok, "hello"}
iex> {1, 2, :true}
```

Because these are created and stored in one block in memory, we can use the indicies to indicate which value we want to pull out of a tuple. For instance, we can get the `:ok` value in the first tuple by looking for the first element:

```elixir
iex> elem({:ok, "hello"}, 0) # :ok
```

We can check the size of a tuple using the `tuple_size/1` function:

```elixir
iex> tuple_size({:ok, "hello"}) # 2
```

And we can replace elements in a tuple by using the `put_elem/3` function, which takes the tuple, the argument, and the value:

```elixir
iex> put_elem({:ok, "hello"}, 1, "world")
```

> Note that Erlang (and thus Elixir) create immutable data. That is, the original tuple is not replaced, but a new tuple based upon the first one is created.
>
> It turns out that even though it feels like a hinderance, using immutable data makes our software easier to reason about and never need to worry about overwriting variables in memory (thus preventing race conditions) and more.
>
> Although we don't need to focus on this now, it's a good idea to keep in mind that no variables is manipulated after it's created, but that a new one is created.
