---
layout: page
title: Creating a Migration
date: 2016-08-15 00:13:42 -0600
position: 6
---

# Goals

<table class="model-diagram">
<thead><tr><th>Topics</th></tr></thead>
<tbody>
<tr><td>id</td></tr>
<tr><td>title</td></tr>
<tr><td>description</td></tr>
</tbody>
</table>


The suggestotron has a list of topics that people can vote on. We'll store our topics in the database. In this step you'll do the following:

* Create a simple Table in the database for topics with a title and a description

* Automatically generate the corresponding Scaffold in Rails (namely, the Model, the View, and the Controller).

#Steps
##Step 1
Type this in the terminal:
```
mix phoenix.gen.html Topic topics description:text title:string
```
`phoenix.gen.html` tells phoenix to create everything we need for a topics page. `Topic` tells phoenix what to call the model, and `topics` tells it what to call the database table.

`title:string` says that topics have a title, which is a "string".
`description:text` says that topics have a description which is a "string". (What's the difference between "string" and "text"? Basically "text" is for strings that might be very long.)
If you want, take some time to poke around the files listed in this step.

Step 2
Type this in the terminal:
```
mix ecto.migrate
```
This tells Phoenix (through the database library, Ecto) to update the database to include a table for our new model.

Explanation
mix

mix is a tool that allows you to run small elixir programs (tasks) that you use often in your application.

Here, `mix ecto.migrate` is a task provided by the Phoenix framework. It uses the migration file we just created (priv/repo/migrations/201xxxxxxxxxxx_create_topics.exs) to change the database. Database migration files can be crucial to code collaboration.

You can run mix -T to see a list of all the rake commands your app currently responds to, along with a short description of each task.
