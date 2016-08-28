---
layout: post
title: learning_elixir
date: 2016-08-28 13:38:30 -0700
---

## Goals

By the end of this section, you'll know:

* The basics of Elixir
* Use the elixir REPL to run elixir code
* Run elixir code from a script
* How to find elixir documentation

## Getting started

We can use the REPL (Read-Eval-Print Loop) command-line tool to write and run simple elixir calculations directly from the command-line. The REPL tool is great for writing simple elixir code, checking on syntax, and understanding how the Elixir run-time works.

Before we move on any further, let's open the Interactive EliXir REPL. After installing Elixir, we'll have at least three new commands. One of these commands is the `iex` command (_I_nteractive _E_li_X_ir), which launches the Interactive EliXir command prompt. 

![eix prompt](/assets/learning_elixir/iex.png)

From this console, we'll be able to play around and experiment with Elixir. Anytime that you see code prepended by the string `iex> `, this means we're working inside the REPL. Feel free to try it along with us as we go. It's a good way to get your fingers working through writing Elixir.

To exit the `iex` prompt, press `Ctrl+c` twice. 

### Notation

In this section, we'll be using a few notations it's good to know about before we start. 

If you see the notation of of a name followed by a `/` and number, this indicates a function and it's number of arguments (arity). 

* `is_integer/1` - indicates a function called `is_integer` that accepts `1` argument

## Official documentation

It's always a great idea to be able to look through documentation when you have a question. Using documentation is often overlooked as a skill and thus, we propose it's a great idea to start with documentation from the beginning.

The official documentation can be found on the [elixir docs](http://elixir-lang.org/docs.html) page. We'll be using the latest _stable_ version of the docs, which can be found on the elixir docs page above and is also available at [http://elixir-lang.org/docs/stable/elixir/Kernel.html](http://elixir-lang.org/docs/stable/elixir/Kernel.html). 

## Types

Although Elixir is not a statically typed language, it does have the concept of types. The basic types we'll work with are:

* Numbers
* Booleans
* Atoms
* Strings
* Anonymous functions
* Lists
* Tuples
* Custom types

We'll use all of these types throughout this course (and you'll use them throughout your Elixir career), so let's look at how to create/use each one.

## Number

A number type comprises the Integer and the Float types. Just like how it sounds, the number types are plain ole' numbers. 

### Integer

In our `eix` command prompt, these are all integers:

```
iex> 1
iex> 200000
iex> 0xA
iex> 0b011
iex> 0x11
```

> [Docs for Integer](http://elixir-lang.org/docs/stable/elixir/Integer.html)

Notice that we can create not only base-10 numbers, but octal, hex, and even binary numbers with elixir and it understands both.

We can check if a value is an integer by using the function `is_integer/1`. For instance:

```
iex> is_integer(1) # true
iex> is_integer(3.14) # false
```

### Floats

Creating/using floats is equally as easy. The difference between a float and an integer is indicated by it's precision. They require a dot followed by at _least_ one digit. These are all floats:

```
iex> 1.0
iex> 2000.8
iex> 1.0e-10
```

We can check if a value is a float by using the `is_float/1` function. 

The built-in number types have functions we can perform on them as well, such as addition, division, mixing precision, and more. 

```
iex> 1 + 1 # 2
iex> div(10, 2)
iex> rem(10, 3)
iex> ## Or without parenthesis
iex> rem 10 3
iex> Float.ceil(1.234567, 3) # 1.235
iex> 10 / 2
```

Try some other commands out to see what else you can do. 

> [Float docs](http://elixir-lang.org/docs/stable/elixir/Float.html)

We can also call functions on these results as well. For instance:

```
iex> is_integer(1 + 1) # true
iex> is_float(div(10, 2)) # false
iex> is_boolean(10 / 2) # false
iex> is_boolean(10 / 2 == 5) # true
```

### Boolean

Booleans are `true` and `false` types. We can use these types to check truth conditions. 

```
iex> true ## true
iex> true == false
```

It's possible to check if a variable is a boolean by using the `is_boolean/1` function:

```
iex> is_boolean(true) # true
iex> is_boolean(1) # false
```

## Atoms

We'll use atoms a lot in Elixir. They are their own constant values. If you're familiar with Ruby, these are symbols. 

For instance, these are all atoms:

```
iex> :hello
iex> :world
iex> true
```

Atoms have their own value in Elixir. We've actually already seen an atomic value in the booleans. Booleans are actually atoms themselves. We can check if a particular value is an atom by using the `is_atom/1` function:

```
iex> is_atom(:hello) # true
iex> is_atom(2.0) # false
iex> is_atom(true) # true
```

## Strings

Strings in Elixir are similar to other languages which are values between _double quotes_ (`"`) and are UTF-8 encoded. For instance, these are all strings:

```
iex> "hello world"
iex> "hello\nworld\n"
```

We can print strings by using the `IO` module (which we'll look at in a few) by using the `IO.puts/1` command. We'll come back to using `IO.puts/1` when we write to files which we'll run. 

Just like integers, the `String` module has a lot of functions built-in to the standard library we can use out of the box. 

```
iex> String.length("hello world") # 11
iex> String.upcase("hello world") # HELLO WORLD
```

We can concatenate strings using the `<>` operator. For instance:

```
iex> "Hello" <> "World" # "HelloWorld"
```

More documentation on the [String](http://elixir-lang.org/docs/stable/elixir/String.html) module is available at [http://elixir-lang.org/docs/stable/elixir/String.html](http://elixir-lang.org/docs/stable/elixir/String.html).

## Anonymous functions

In Elixir, we can create functions which are treated just like any other type in Elixir. To create a function, we'll use the keywords of `fn` and `end`. 

For instance, all of these are functions in Elixir:

```
iex> add = fn a, b -> a + b end
iex> is_function(add) # true
iex> b = (fn a -> a + 2 end)
```

In order to actually execute our anonymous functions, we'll need to add a suffix of `.` to the end of the function name. For example, to call the `add/2` function, we'll need to type:

```
iex> add.(2 2) # 4
```

## Lists

Lists in Elixir are created by surrounding a list of values with brackets `[`. Lists don't need to contain only one type. They can hold on to multiple different types in the same list. 

For instance, these are all _valid_ lists:

```
iex> [1, 2, 3]
iex> [:hello, "world"]
```

We have a bunch of built-in methods we can use to interact with and manipulate lists in Elixir. 

```
iex> length [1, 2, 3] # 3
iex> [1] ++ [2] # [1, 2]
iex> [1, 2, 3] -- [2] # [1, 3]
```

Common functions we'll use whenever we write Elixir code are checking for the head (`hd/1`) and tails of a list (`tl/1`). When we talk about the head of the list, we're looking for the first element of the list. For instance:

```
iex> hd([1, 2, 3]) # 1
```

The tail is everything _but_ the head of the list:

```
iex> tl([1, 2, 3]) # [2, 3]
```

In Elixir, we'll often work with lists an element at a time, so the `hd/1` command will come in handy. 

## Tuples

Tuples in Elixir are used to store elements contiguously in memory, which means we can get elements in the tuple by it's place within the tuple. Before we get too far ahead of oursevles, let's look at how to create a tuple.

Tuples are created by using the curly brackets with elements separated by commas. These are all tuples in Elixir:

```
iex> {:ok, "hello"}
iex> {1, 2, :true}
```

Because these are created and stored in one block in memory, we can use the indicies to indicate which value we want to pull out of a tuple. For instance, we can get the `:ok` value in the first tuple by looking for the first element:

```
iex> elem({:ok, "hello"}, 0) # :ok
```

We can check the size of a tuple using the `tuple_size/1` function:

```
iex> tuple_size({:ok, "hello"}) # 2
```

And we can replace elements in a tuple by using the `put_elem/3` function, which takes the tuple, the argument, and the value:

```
iex> put_elem({:ok, "hello"}, 1, "world")
```

> Note that Erlang (and thus Elixir) create immutable data. That is, the original tuple is not replaced, but a new tuple based upon the first one is created. 
> 
> It turns out that even though it feels like a hinderance, using immutable data makes our software easier to reason about and never need to worry about overwriting variables in memory (thus preventing race conditions) and more.
> 
> Although we don't need to focus on this now, it's a good idea to keep in mind that no variables is manipulated after it's created, but that a new one is created. 

## Operators

Elixir has a lot of built-in operators. We've already seen a few, such as addition (`+`), division (`/`), and `++`/`--` (list manipulation):

```
iex> [1, 2, 3] ++ [4, 5, 6] # [1, 2, 3, 4, 5, 6]
iex> [1, 2, 3] -- [2] # [1, 3]
iex> "Hello" <> "World" # HelloWorld
```

We can also check for boolean operators, such as using `and`, `or`, and `not`. We need to use a boolean as the first argument of these operators. For instance:

```
iex> true and true # true
iex> false or is_atom(:example) # true
```

The `or` and `and` operators are called _short-circut_ operators as they execute the left-side first and if it is enough, the right-hand side will not be executed. 

```
iex> false and raise("Error") # false
iex> true or raise("Error")
```

We can use the `||`, `&&`, and `!` operators which accept arguments of all types. All values from these operators evaluate to true except for `false` and `nil`. 

```
iex> 1 || true # 1
iex> nil && 13 # nil
iex> !1 # false
```

We can check equality using the `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<`, and `>` comparison operators. The `==` operator and `===` have different levels of strict-ness, where the `==` operator is less restrictive:

```
iex> 1 == 1.0 # true
iex> 1 === 1.0 # false
```

## Variables

In Elixir, we'll use variables all over the place. In Elixir, we can create variables simply by setting the _name_ of a variable equal to it's value using the `=` operator:

```
iex> a = 1 # 1
iex> list = [1, 2, 3]
iex> tuple = {:ok, "Hello"}
```

## Pattern matching

One of the more powerful ideas in Erlang (and therefore Elixir) is using destructuring and pattern matching. To handle these concepts, Elixir allows us to break up lists by their placement. For instance:

```
iex> [a, b, c] = [1, 2, 3]
iex> a # 1
iex> c # 3
```

We'll also use the head and tail operators to get a list's head and tail elements in a destructured way:

```
iex> [ head | tail] = [1, 2, 3] # [1, 2, 3]
iex> head # 1
iex> tail # [2, 3]
iex> ## We can also preprend values using this destructuring
iex> [1 | [2, 3]] # [1, 2, 3]
```

Lists aren't the only data structure that allows us to pattern match. We can pattern match on tuples as well. For instance:

```
iex> {a, b, c} = {:hello, "world", 42}
iex> a # :hello
iex> c # 42
```

> This works as the tuples are the same size. We'll get a `MatchError` if the size of the tuples are different
>
> ```
> {a, b, c} = {:ok, "hello"} # MatchError
> ```

We'll also use pattern matching to match on specific values of a tuple. This is incredibly useful for checking results of functions, for instance.

```
iex> {:ok, msg} = {:ok, "Hello world"}
iex> msg # "Hello world"
```

If we are only interested in a single value in a pattern, we'll use the `_` notation which is a common way of saying we don't have need for this value in a pattern. For instance, a common usecase is if we want to only get the head of a list. 

```
iex> [head | _] = [1, 2, 3]
iex> head # 1
```

## Control structures

We often want to run a check on a particular state of a variable. 

### `case`

The `case` function allows us to compare a value against several patters until we find one that matches. For instance:

```
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

```
iex> case {1, 2, 3} do
    {1, x, 3} when x > 0 ->
        "Matches"
    _ -> 
        "Matches if the guard condition is false"
    end
```

We can use lots of different operators in the guard clauses above. The documentation at [http://elixir-lang.org/getting-started/case-cond-and-if.html#expressions-in-guard-clauses](http://elixir-lang.org/getting-started/case-cond-and-if.html#expressions-in-guard-clauses) is pretty complete and covers all of the operators we have available to us.

If there are no matching clauses in a `case` statement, an error will be raised:

```
iex> case :ok do
      :error -> "Does not match"
    end
```

### `cond`

The `cond` function allows us to check against the conditions which evaluate to true rather than just different values. It's similar to the `case` statement, but evaluates functions and uses it's result to pattern match:

```
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

```
iex> if true do
      "This is true"
     end
iex> unless true do
      "This won't be seen"
     end
```

We can also use `else` in our `if` and `unless` blocks as well:

```
iex> if false do
        "This won't be seen"
     else
        "This will be seen"
     end
```

### `do/end` blocks

We've seen the `do/end` blocks in our previous operators. They allow us to define the start and end block to be executed if a condition has been met. For instance:

```
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

## keyword lists

We'll often want to set up a 2-item tuple as a representation of a `key-value` data structure. 

> In languages like Python, this is similar to a dictionary.

For instance, if we want to set up a key-value mapping, we set them as a list of tuples from the first item to the second. For instance:

```
iex> list = [{:a, 1}, {:b, 2}]
iex> list[:a] # 1
iex> list[:c] # nil
```

We can concatenate the dictionary using the key-value syntax woth `++`. For instance:

```
iex> list = [{:a, 1}, {:b, 2}]
iex> list[:a] # 1
iex> list[:c] # nil
iex> newList = list ++ [c: 3]
iex> newList[:c] # 3
iex> list[:c] # nil
```

We'll use keyword-lists a lot in [Ecto](https://github.com/elixir-ecto/ecto) (the database wrapper of the Phoenix library) to make elegant queries to our database. We'll come back to this in a little while.

Keyword lists are just lists which means that this isn't really a fantastic data structure for doing large operations against. For this reason, Elixir provides another data structure: the `Map`.

## Maps

Maps in Elixir provides a quick key-value store called a map. Maps can be created by using the `%{}` syntax:

```
iex> map = %{:a => 1, 2 => :b}
iex> map[:a] # 1
iex> map[2] # :b
iex> # We can use the . syntax to access variables too
iex> map.c # nil
```

Maps do not contain ordering and can allow _any_ value to be set as the key. 

## Nested data structures

Elixir provides a way for us to hold variables inside of maps. We'll use this all over the place in Phoenix, where we'll have variables that represent data structures in our database. For instance, we can create a list of users that is a key-value map to another nested map:

```
iex> users = [
  john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
  mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
]
```

We can then get variables using the `[]` and `.` syntax:

```
iex> users[:john].age # 27
```

We can then manipulate variables by using the `put_in/2` function to create a new value:

```
iex> users = put_in users[:john].age, 31
iex> users # 
john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
```

It's _also_ possible to define how to manipulate the value using the `update_in/2` function. 

```
iex> users = update_in users[:mary].languages, &List.delete(&1, "Clojure")
[john: %{age: 31, languages: ["Erlang", "Ruby", "Elixir"], name: "John"},
 mary: %{age: 29, languages: ["Elixir", "F#"], name: "Mary"}]
```

Check out the [Kernel module](http://elixir-lang.org/docs/stable/elixir/Kernel.html) documentation for more information on other functions available to use when using nested datastructures. 

## Executing scripts

// TODO: 

