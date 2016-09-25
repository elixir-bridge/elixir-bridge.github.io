---
layout: post
title: Running the Application Locally
date: 2016-08-15 00:08:57 -0600
---

Goals
Let's fire up the application locally

# Steps
##Step 1
Make sure that you're in the suggestotron folder. You can type `pwd` (print working directory) in the terminal to see what folder you are in.

Type this in the terminal:

```
mix phoenix.server
```

This will print some stuff and stay running forever, printing more stuff every time you visit a page in your app.

Expected result:
```
Compiled web/views/topic_view.ex
[info] Running TestApp.Endpoint with Cowboy using http on port 4000
11 Sep 17:57:34 - info: compiled 5 files into 2 files, copied 3 in 1.2 sec

```

##Step 2
Point your web browser to http://localhost:4000
See your web app actually running!

##Step 3
While the server is running, whatever you type in that terminal tab will be ignored.

To get back to the terminal, you can stop the server by typing Control-c twice.


Explanation
`mix phoenix.server` ran your application locally just like Heroku will be running it on their servers.

This provides a very simple means to see your changes before you commit and push them to Heroku.

Control-c is a way of closing or cancelling terminal programs. Since the phoenix server runs forever, you need to interrupt it with Control-c.

## Next Step
Go on to [Creating a Migration](/suggestotron/06-creating-a-migration.html)
or,
Go Back to [Add the Project to a Git Repo](TODO: FILL ME IN)
