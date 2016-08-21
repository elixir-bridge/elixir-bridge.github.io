---
layout: post
title: Create a Phoenix App
date: 2016-08-21 12:28:28 -0700
---

### Step 1: Change to your home directory

#### Mac or Linux
Type this in the terminal:
```
cd ~
```

`cd ~` sets our home directory to our current directory.

### Step 2: Create an Elixirbridge directory

To keep things organized, we'll want all of the elixirbridge files in their own directory. Type this in the terminal:
```
mkdir elixirbridge
```
`mkdir` stands for make directory (folder).

We've made a folder called elixirbridge.

### Step 3:
Change to your new elixirbridge directory
Type this in the terminal:
```
cd elixirbridge
```
### Step 4: Create a new Phoenix app
Type this in the terminal:

```
mix phoenix.new test_app
```

The command's output is a list of the files it creates, which will be fairly long. We'll go into detail about what these files are later. Then it will as you to fetch and install dependencies, type `Y` to do this. If there's an error at this point, grab a volunteer to help you.

Change into the project directory:

```
cd test_app
```

#### Create the database

Type this in a terminal:
```
mix ecto.create
```

Then, type this in a terminal:
```
mix phoenix.server
```

If phoenix server starts up with no errors, you're golden! It'll look something like this:

```
[info] Running TestApp.Endpoint with Cowboy using http://localhost:4000
21 Aug 13:06:41 - info: compiled 6 files into 2 files, copied 3 in 958ms
```

In your browser, open [localhost:4000](http://localhost:4000). You should see a page Like this:

(TODO: insert screenshot here)
![](/assets/welcome-to-phoenix.png)




##### Scratch
install node/ check if they hve it
`npm install && node node_modules/brunch/bin/brunch build`