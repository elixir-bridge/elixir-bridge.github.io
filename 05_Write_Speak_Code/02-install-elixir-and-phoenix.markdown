---
layout: page
title: Install Elixir and Phoenix
date: 2016-09-24 12:28:28 -0700
---


### Step 1: Install Elixir

You can either install elixir with asdf or brew. We recommend asdf, but either approach will be sufficient.

### asdf

For asdf follow the setup instructions here - [https://github.com/asdf-vm/asdf](https://github.com/asdf-vm/asdf)

#### Homebrew

Before installing anything with homebrew, always update to latest,
by typing this in the terminal:

`brew update`

then you can use homebrew to install elixir:

 `brew install elixir`

#### OR Macports

Alternately, you may install using Macports, by typing this in the terminal:

`sudo port install elixir`

#### Windows installation

Navigate to [https://chocolatey.org/install](https://chocolatey.org/install).

Install the chocolatey package.

Then install elixir. Follow the instructions here: [https://chocolatey.org/packages/Elixir](https://chocolatey.org/packages/Elixir)

#### Check Your Installation

To check that Elixir is installed correctly:

`elixir -v`

You should see a version number greater than 1.5, like this:

`Elixir 1.5.1`

Anything above 1.5 is fine.

### Step 2: Install Hex

Type this in the terminal:

```
mix local.hex
```
