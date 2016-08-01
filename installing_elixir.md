---
layout: post
title:  "Installing Elixir"
date:   2016-07-30 10:55:36 -0700
categories: elixir, install_elixir, mac, linux, windows, compile
---
##Installing Elixir

The Elixir team has done an excellent job of making Elixir easy to install on just about every major platform.  For users comfortable with their computer and operating system, the [Installing Elixir](http://elixir-lang.org/install.html) guide should be sufficient.  

For more detailed instructions,  see the guides below.

###Mac
The easiest way to install Elixir on a Mac is to use homebrew.  

[Homebrew](http://brew.sh/) is a package manager for OS X.  It installs commonly used programs that don't come preinstalled.  Additionally, when new versions of programs are released, they can be updated easily with Homebrew.  

To install homebrew, open the Terminal app (or iterm) and copy the following line:

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

If you're skeptical of running random commands posted on websites, feel free to check out the [source code](https://github.com/Homebrew/brew/).  

Once brew has installed, run `brew doctor` to make sure that everything has been installed correctly.  

Then simply run, `brew install elixir` and you'll have the latest version of Elixir installed.  Since Elixir runs on top of the Erlang VM, brew will also install Erlang 18 or Erlang 19. 

To ensure Elixir has been installed correctly, run the following command: `elixir -v`.  The output should look 
something like this:

```
Erlang/OTP 18 [erts-7.2.1] [source] [64-bit] [smp:8:8] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Elixir 1.3.1
```

###Windows
Installing Elixir on Windows is very straightforward.  Download the [installer](https://repo.hex.pm/elixir-websetup.exe) and follow the prompts.  

This package should also install Erlang.  In the event that it doesn't see the [Installing Erlang](#installing-erlang) section at the bottom.

To ensure Elixir has been installed correctly, run the following command: `elixir -v`.  The output should look 
something like this:

```
Erlang/OTP 18 [erts-7.2.1] [source] [64-bit] [smp:8:8] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Elixir 1.3.1
```

###Linux

###Compile

###Elixir Version Managers

###Installing Erlang
<a name="installing-erlang">Installing Erlang<a>

