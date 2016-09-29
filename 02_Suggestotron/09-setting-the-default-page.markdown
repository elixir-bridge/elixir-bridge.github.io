---
layout: page
title: Setting the Default Page
date: 2016-08-28 11:38:51 -0700
position: 9
---

## Goals
Now that the structure is complete, let's make the flow work smoothly.

Currently when you go to http://localhost:4000 you see the "Welcome aboard" message.

It would be easier to use our app if http://localhost:4000 went directly to the topics list.

In this step we'll make that happen and learn a bit about routes in Rails.

## Steps
* Step 1: Add a root route

Open the file `web/router.ex` in an editor (In the InstallFest yesterday, we suggested that you install and use Atom as your editor).

Look for the line `get "/", PageController, :index` in the lower two thirds of the file, and change `PageController` to say `TopicController`. When you are done that block of code should look like this:

```scope "/", TestApp do
  pipe_through :browser # Use the default browser stack

  resources "/topics", TopicController
  get "/", TopicController, :index
end
```

Step 2: Confirm your changes
Go back to http://localhost:4000/. You should be taken to the topics list automatically.

Explanation

`get "/", TopicController, :index` is a Phoenix route that tells the app when a GET request comes in for the root of the site (that is, the domain without anything after the /), to user the `TopicController` and the `:index` method. The `index` method is the topics list page.

Phoenix routes control how URLs get matched with the code on the server. It's similar to how houses and apartments have addresses. You can think of each controller as a street, and each method in that controller as a house.

The file `web/router.ex` is like an address directory listing all the possible addresses and which code goes with each one. `routes.rb` uses some shortcuts so that it doesn't always show all the possible URLs. To explore the URLs in more detail we can use the terminal.

At the terminal type `mix phoenix.routes`. You should get something that looks like this:

```
$ mix phoenix.routes
topic_path  GET     /topics           TestApp.TopicController :index
topic_path  GET     /topics/:id/edit  TestApp.TopicController :edit
topic_path  GET     /topics/new       TestApp.TopicController :new
topic_path  GET     /topics/:id       TestApp.TopicController :show
topic_path  POST    /topics           TestApp.TopicController :create
topic_path  PATCH   /topics/:id       TestApp.TopicController :update
            PUT     /topics/:id       TestApp.TopicController :update
topic_path  DELETE  /topics/:id       TestApp.TopicController :delete
topic_path  GET     /                 TestApp.TopicController :index
```
This shows all the URLs your application responds to. The parts of the URLs that start with colons are variables so :id means the id number of the record.

Deploying
Before the next step, you could try deploying your app to Heroku!

Go on to Deploying To Heroku
