---
layout: page
title: Keyword Lists
date: 2016-10-1 13:38:30 -0700
---

## keyword lists

We'll often want to set up a 2-item tuple as a representation of a `key-value` data structure.

For instance, if we want to set up a key-value mapping, we set them as a list of tuples from the first item to the second. For instance:

```elixir
iex> list = [a: 1, b: 2]
iex> list[:a] # 1
iex> list[:c] # nil
```

Since keyword lists are just lists, we can use all available operators to lists. For instance, we can use `++` to add new values:

```elixir
iex> list = [a: 1, b: 2]
iex> list[:a] # 1
iex> list[:c] # nil
iex> newList = list ++ [c: 3]
iex> newList[:c] # 3
iex> list[:c] # nil
```

We'll use keyword lists a lot with [the Ecto library](https://github.com/elixir-ecto/ecto) for writing queries and interacting with databases in Elixir. Ecto is the database wrapper used by the Phoenix framework and will be covered in that class.

Keyword lists are not really a fantastic data structure for doing large operations. For this reason, Elixir provides another data structure called maps which is considered the "go to" data structure whenever you need a key-value store.
