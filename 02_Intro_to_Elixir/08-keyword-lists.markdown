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

We can concatenate the dictionary using the key-value syntax with `++`. For instance:

```elixir
iex> list = [a: 1, b: 2]
iex> list[:a] # 1
iex> list[:c] # nil
iex> newList = list ++ [c: 3]
iex> newList[:c] # 3
iex> list[:c] # nil
```

We'll use keyword-lists a lot in [Ecto](https://github.com/elixir-ecto/ecto) (the database wrapper of the Phoenix library) to make elegant queries to our database. This is covered in the Phoenix class in more depth.

Keyword lists are just lists which means that this isn't really a fantastic data structure for doing large operations.  For this reason, Elixir provides another data structure: the `Map`.
