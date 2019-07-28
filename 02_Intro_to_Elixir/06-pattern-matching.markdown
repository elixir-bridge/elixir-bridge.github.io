---
layout: page
title: Pattern Matching
date: 2016-10-1 13:38:30 -0700
---


## Pattern matching

One of the more powerful ideas in Elixir is using pattern matching. In Elixir the `=` acts as the match operator.
The term on the right matches the pattern on the left. If there is a match we return the value of the pattern, otherwise we get an error. Lets look at an example

```elixir
a = 1
1 = a
```

If we look above, the first line looks

```elixir
a = 1
```

It may look like assignment if you are familiar with object oriented languages.

However what is actually happening is `a` initially does not have a value, so with uninitialized variables, the variable gets bound to the value on the right hand side of the expression. We can pretend it works like assignment for now.

In the next line we now know `a` has a value of 1. Here we are checking that the term on the right, matches the pattern on the left.

Since `a` has a value of 1

```elixir
1 = a
```

is equivalent to

```elixir
1 = 1
```

So we have a match.

 We talked about variables matching anything you put on the right of the equals sign. Let's take a look at another example:

```elixir
list = [1,2,3]
```

The variable `list` is now bound to the term `[1,2,3]`.

You can use more complex patterns for when you just want to match part of a data structure. To handle these concepts, Elixir allows us to break up lists by their placement. Type the following into `iex`:

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

### Review of Head and Tail

Often times we have a list, but we only care about the first item.

Remember when we looked at the `head` and `tail` of the list? This was pattern matching.

 Elixir gives us the `[first_item|remaining_items]` pattern, where the `first_item` gives us the first item in the list, and the `remaining_items` is a sub-list with the remaining items. Those variables can be any name you want; the pipe (`|`) is what makes the pattern work. Try it out:

```elixir
iex> [ head | tail] = [1, 2, 3]
[1, 2, 3]
iex> head
1
iex> tail
[2, 3]
```

You can also add to the beginning of a list this way. Try the following:

```elixir
iex> [1 | [2, 3]]
[1, 2, 3]
```

### Ignoring Values

If we are only interested in a single value in a pattern, we'll use the `_` notation which is a common way of saying we don't have need for this value in a pattern. For instance, a common use case is if we want to only get the head of a list.

```elixir
iex> [head | _] = [1, 2, 3]
iex> head
1
```

### Pattern Matching with Tuples

Lists aren't the only data structure that allows us to pattern match. Tuples are data structures used for a fixed number of items. We can pattern match on tuples as well. For instance:

```elixir
iex> {a, b, c} = {:hello, "world", 42}
iex> a
:hello
iex> c
42
```

This works as the tuples are the same size. We'll get a `MatchError` if the size of the tuples are different. Type the following:

```elixir
iex> {a, b, c} = {:ok, "hello"}
```

What happened? You should have seen something like:

```elixir
iex(5)> {a, b, c} = {:ok, "hello"}
** (MatchError) no match of right hand side value: {:ok, "hello"}
```

### Matching on specific values of a Tuple

We'll also use pattern matching to match on specific values of a tuple. Try the following:

```elixir
iex> {:ok, msg} = {:ok, "hello"}
iex> msg
"hello"
```

This is incredibly useful for checking results of functions; many libraries allow you to deal with errors this way. In this example, we use a case statement to match the result of a web request. We'll talk more about `case` when we talk about control structures.

```elixir
case HttpPoison.get('example.com') do
  {:ok, result} ->
    result
  {:error, some_error} ->
    handle_error
end
```

Pattern matching can be used with any of the data types built into elixir. You'll see more examples of this as we move along.

### Pin Operator

One last note on variables in Elixir. In Elixir we can place a pin `^` operator in front of a variable. We do this when we want to match against the contents of the variable.
In other words, we want to keep the value of the variable, rather than bind that variable to a new value.

Let's look at the following code snippet

```elixir
x = 1
 ^x = 2
```

In the snippet above we see that `x` has a value of `1`.

When we try to match the `2` against the value of `x` which is 1, we get an error. When we use the pin operator we can imagine we are replacing the variable with it's value. In which case the above expression would look like this:

```elixir
1 = 2
```
