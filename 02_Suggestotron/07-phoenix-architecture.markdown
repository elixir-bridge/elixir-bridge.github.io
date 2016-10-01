---
layout: page
title: Phoenix architecture
date: 2016-08-15 00:13:42 -0600
position: 7
---

# Goals

By the end of this section, you'll understand the Phoenix architecture, how it works, and the different options we have available to us provided by the Phoenix framework.

The Phoenix framework comprises several parts, each handling their own roles.

* Endpoints
* Router
* Controllers
* Views/Templates
* Channels
* Pubsub
* Plug
* Ecto

Let's look at each one of these and their roles in the Phoenix and how to interact with them.

## Endpoints

An endpoint is the receiver of the HTTP requests and handles dealing with them until it hands off the request to the Router. It provides common interface of plugs to every request and is responsible for dispatching the requests to the appropriate router.

An endpoint is created automatically for us when we run the phoenix webserver using the `mix phoenix.server` command.

## Router

The endpoint hands requests off to the router, which is responsible for accepting the request and dispatching it to the correct controller/action. It takes the request and parses it, splits up parameters and calls the appropriate controller action where necessary.

The router provides some helpers for generating paths to map to a set of resources we'll create with the controllers/actions.

## Controllers

Controllers are at the heart of Phoenix applications. These controllers provide _actions_ which handle requests. They are responsible for preparing data and sending it along to the views to be rendered by the browser.

We'll create controllers with actions to start the rendering process which will be passed along to the browser as a view. Actions, as with other MVC frameworks, such as [Rails](http://rubyonrails.org/) can perform redirects and invoke rendering on the server.

## Views/Templates

The presentation layer of Phoenix, views render templates to be passed along to the browser. They define helper functions which are provided to the templates to allow us to decorate data in the presentation by the browser.

The templates that are rendered by the view are precompiled by the Phoenix compiler and are intended to be fast.

## Channels

We'll work through building a channel with our Phoenix application when we start working through building a chat application. These are responsibile for managing socket requests for _real-time_ communication. They are eseentially controllers, except that instead of only accepting a request, they can allow bi-directional communication with persistent socket connections.

## Pubsub

The pubsub system in Phoenix powers the channel layer which allows clients to _listen_/_subscribe_ to topics and be sent a message when there is something new to know. Since Phoenix was built with extensibility in mind, it abstracts pubsub so third-party pubsub endpoints can be easiy written and extend the exisiting functionality.

We'll work through building a pubsub endpoint in our chat application.

## Plug

A _plug_ is a reusable module which is used for building a composable modules to build our applications. They are intended on providing discrete, understandable behaviors, such as request header parsing and logging.

The plug API is limited and consistent, so plugs can be executed in a concrete order to build a pipeline for processing requests. They can be written once and reused within a single project or multiple projects. Plugs can handle almost anything, from authentication to rendering.

The _plug_ is one secret sauce to Phoenix's extensibility and functionality.

## Ecto

Ecto is another exciting feature of Phoenix which provides a language-integrated query composition database wrapper for Elixir. Essentially, it allows us to read and to write to different databases (similar to ActiveRecord for Rails). It allows us to model our data so that we can easily write complex queries in a type-safe way, while protecting our database from attacks.

It's built around four main abstractions:

* Repo is a connection to an individual database. Every database operation is executed through the repo.
* Model is how we define data. They define table names, fields, and relationships to other models.
* Queries tie models and repositories together, allowing us to retrieve data from a repo and turn it into a model itself.
* Changesets declare data transformations we'll need to perform on our model's data, including operations such as type-casting and validations.

We'll work through these concepts through the guides. For any conceptual questions, feel free to ask a volunteer out for a deeper explanation.
