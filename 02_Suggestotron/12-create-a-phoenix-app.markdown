---
layout: post
title: Create a Phoenix App
date: 2016-09-24 23:08:17 -0700
---

### Step 1: Create a new Phoenix app
Type this in the terminal:

```
mix phoenix.new test_app
```


The command's output is a list of the files it creates, which will be fairly long. We'll go into detail about what these files are later.

![phoenix app output](/assets/phoenix-new-app-output.png)


Then it will ask you to fetch and install dependencies, type `Y` to do this. If there's an error at this point, grab a volunteer to help you.

Change into the project directory:

```
cd test_app
```


### Step 2: Get Dependencies

Type the following into your terminal:

```
mix deps.get
```

Step 6: Install nm and node

```
npm install && node node_modules/brunch/bin/brunch build
```

#### Step 3: Create the database

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

![](/assets/welcome-to-phoenix.png)


Hit `Ctrl c` twice to stop the server


Next Step: [Create a Migration](04-create-a-migration.html)

Go Back: [Getting Started](02-getting-started.html)


