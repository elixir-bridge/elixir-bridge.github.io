---
layout: page
title: Pattern Matching
date: 2016-10-1 13:38:30 -0700
---


## Pattern matching

One of the more powerful ideas in Elixir is using pattern matching for destructuring, or extracting parts of a data structure. As mentioned in the previous section, the `=` sign is the match operator. We talked about variables matching anything you put on the right of the equals sign. Let's take a look at another example:

```elixir
list = [1,2,3]
```
So again, the varianle `list` is now bound to the pattern `[1,2,3]`.

You can use more complex patterns for when you just want part if a data structure. Let's take a look the following example. To handle these concepts, Elixir allows us to break up lists by their placement. Type the following into `iex`:

```elixir
iex> [a, b, c] = [1, 2, 3]
```
What values do these variables now have? Try it:

```elixir
iex(1)> [a, b, c] = [1, 2, 3]
[1, 2, 3]
iex(2)> a
1
iex(3)> b
2
iex(4)> c
3
```

As you can see, it bound the variables in each place to the respective values in the pattern.

Often times we have a list, but we only care about the first item. Elixir gives us the `[first_item|remaining_items]` pattern, where the `first_item` gives us the first item in the list, and the `remaining_items` is a sub-list with the remaining items. Those variables can be any name you want; the pipe (`|`) is what makes the pattern work. Try it out:

```elixir
iex> [ head | tail] = [1, 2, 3] # [1, 2, 3]
iex> head # 1
iex> tail # [2, 3]
```

You can also add to the beginning of a list this way. Try the following:

```elixir
iex> [1 | [2, 3]] # [1, 2, 3]
```

If we are only interested in a single value in a pattern, we'll use the `_` notation which is a common way of saying we don't have need for this value in a pattern. For instance, a common use case is if we want to only get the head of a list.

```elixir
iex> [head | _] = [1, 2, 3]
iex> head # 1
```

Lists aren't the only data structure that allows us to pattern match. Tuples are data structures used for a fixed number of items. We can pattern match on tuples as well. For instance:

```elixir
iex> {a, b, c} = {:hello, "world", 42}
iex> a # :hello
iex> c # 42
```

This works as the tuples are the same size. We'll get a `MatchError` if the size of the tuples are different. Type the following:

```elixir
iex> {a, b, c} = {:ok, "hello"}
```

What happened? You should have seen something like the following:

```elixir
iex(5)> {a, b, c} = {:ok, "hello"}
** (MatchError) no match of right hand side value: {:ok, "hello"}
```

We'll also use pattern matching to match on specific values of a tuple. Try the following:

```elixir
iex> {:ok, msg} = {:ok, "hello"}
iex> msg # "Hello world"
```
This is incredibly useful for checking results of functions; many libraries allow you to deal with errors this way. In this example, we use a case statement to match the result of a web request. We'll talk more about `case` when we talk about control structures.

```elixir
case HttpPoison.get('example.com') do
  {:ok, result}
    result
  {:error, some_error}
    handle_error
  end
end
```

Pattern matching can be used with any of the data types built into elixir. You'll see more examples of this as we move along.

### Tuples or Lists?

When do we use a list and when a tuple? It is good to kep in minde that lists are slow to moify/read but fast to create. Tuples aer expensive to modify, but are good at handling pattern matching and returning additional info.


