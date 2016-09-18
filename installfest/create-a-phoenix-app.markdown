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

Now type this into the terminal:

```
which node
```

You should see something like this in your terminal:

```
/usr/local/bin/node
```

If you do see this, move on to the next step.
Otherwise type the following into your terminal:

```
brew install node
```

### Step 5:

Type the following into your terminal:

```
mix deps.get
```

### Step 6:

```
npm install && node node_modules/brunch/bin/brunch build
```

### Step 7: Create the database

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

![Welcome to Phoenix](/assets/welcome-to-phoenix.png)


It works! Go back to your Terminal window and type Control-c to stop the server for now.


### Step 8: Generate a database model

If your prompt doesn't already show you that you are in your test_app folder type

```
cd test_app
```

```
mix phoenix.gen.html Drink drinks title:string temperature:string
```

You should see output similar to this:

```
* creating web/controllers/drink_controller.ex
* creating web/templates/drink/edit.html.eex
* creating web/templates/drink/form.html.eex
* creating web/templates/drink/index.html.eex
* creating web/templates/drink/new.html.eex
* creating web/templates/drink/show.html.eex
* creating web/views/drink_view.ex
* creating test/controllers/drink_controller_test.exs
* creating web/models/drink.ex
* creating test/models/drink_test.exs
* creating priv/repo/migrations/20160828191433_create_drink.exs

Add the resource to your browser scope in web/router.ex:

    resources "/drinks", DrinkController

Remember to update your repository by running migrations:

    mix ecto.migrate
```

Now let's follow the instructions at the end of that output.

We'll add routes. Launch Atom and open up a file named 'web/router.ex'

Around line 19 (this will vary depending on your editor)

delete the section that looks like

```
 scope "/", TestApp do
    pipe_through :browser # Use the default browser stack

    get "/", PageController, :index

    resources "/pages", PageController
  end
```
and paste in the following

```
scope "/", TestApp do
    pipe_through :browser # Use the default browser stack

    get "/", DrinkController, :index

    resources "/drinks", DrinkController
  end
```

Now type this into the terminal

```
mix ecto.migrate

```

Lets start start our server up again

Type the following into the terminal

```
mix phoenix.server
```

Wait till your server has loaded like before.

Then in the browser url bar type in:
```
http://localhost:4000/drinks
```

1. Click on new drink
2. Enter Cappuccino for the name
3. Enter 135 for the temperature.
4. Click on "Create Drink".

You should see the following text at the top of the page

![drinks successfully created ](/assets/drinks-created.png)














