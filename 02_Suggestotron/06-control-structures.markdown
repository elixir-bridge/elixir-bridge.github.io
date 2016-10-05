## Control structures

We often want to run a check on a particular state of a variable.

### `case`

The `case` function allows us to compare a value against several patters until we find one that matches. For instance:

```elixir
iex> case {1, 2, 3} do
    {4, 5, 6} ->
        "Does not match"
    {1, x, 3} ->
        "This caluse does match and sets x to 2"
    _ ->
        "Matches any value not previously matched"
    end
```

We can also use _guards_ to check against extra conditions in a `case` statement. This is useful for setting _extra_ conditions not previously covered in the match statement:

```elixir
iex> case {1, 2, 3} do
    {1, x, 3} when x > 0 ->
        "Matches"
    _ ->
        "Matches if the guard condition is false"
    end
```

We can use lots of different operators in the guard clauses above. The documentation at [http://elixir-lang.org/getting-started/case-cond-and-if.html#expressions-in-guard-clauses](http://elixir-lang.org/getting-started/case-cond-and-if.html#expressions-in-guard-clauses) is pretty complete and covers all of the operators we have available to us.

If there are no matching clauses in a `case` statement, an error will be raised:

```elixir
iex> case :ok do
      :error -> "Does not match"
    end
```

### `cond`

The `cond` function allows us to check against the conditions which evaluate to true rather than just different values. It's similar to the `case` statement, but evaluates functions and uses it's result to pattern match:

```elixir
iex> cond do
      2 + 2 == 5 ->
        "This is not true"
      2 * 2 == 3 ->
        "This is not true"
      1 + 1 == 2 ->
        "This does match"
    end
```

### `if` and `unless`

We can check a single value by using the `if` and `unless`.

```elixir
iex> if true do
      "This is true"
     end
iex> unless true do
      "This won't be seen"
     end
```

We can also use `else` in our `if` and `unless` blocks as well:

```elixir
iex> if false do
        "This won't be seen"
     else
        "This will be seen"
     end
```

### `do/end` blocks

We've seen the `do/end` blocks in our previous operators. They allow us to define the start and end block to be executed if a condition has been met. For instance:

```elixir
iex> if true do
        a = 1 + 2
        a + 10
     end
iex> # And the equivalent using :
iex> if true, do: (
        a = 1 + 2
        a + 10
     )
```
