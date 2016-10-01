---
layout: page
title: CRUD with scaffolding
date: 2016-08-21 13:39:33 -0700
position: 8
---

Goals
At the core, most database driven web sites are the same. They need to store records and provide a way to do the following:

* Create new records in the database
* Read or show the records in the database
* Update existing records
* Destroy or delete records

Because these 4 actions (CRUD) are so common, Phoenix includes the scaffold command to make creating them easier.

### Steps

#### Step 1

* Type this in the terminal:
```
mix phoenix.server
```

#### Step 2
Point your browser to http://localhost:4000/topics

Screenshot of topic list page:
![Screenshot of topics Page](/assets/topics-screenshot.png)

#### Step 3
* Click "New Topic"
* Fill in the form and click "Submit"

You should see the list page, with your new topic listed and with a message that your topic was successfully created:

![Screenshot of topics Page](/assets/topics-created-screenshot.png)

Try the "Show", "Edit", and "Destroy" links to see what they do
You've created a basic database driven web site, congrats!

### Explanation
How did all those pages get created and hooked together? The Phoenix scaffold did it for you.

Let's take a closer look at some of the files Phoenix created:

```
web/models/topic.ex
```

This file contains code for our topic model. If you look at it, it contains information about the columns we specified in our `phoenix.gen.html` command in the last step, and not much else. Creating, reading, updating, and deleting records are built into Phoenix.

```
web/templates/topic
```
This folder contains all the views for our topics model. This is where the code for the forms you used above is stored. Phoenix created all of these pages as part of the scaffold.
If you've written HTML before, many lines in the views should look familiar. Phoenix views are HTML with some extra code added to display data from the database.

```
web/templates/topic/index.html.eex
```
This is the code for the page that lists all the topics.
Index is the name given to the "default" page for a web site or a section of a web site. When you navigate to http://localhost:3000/topics the topics index page is what is sent to your computer.

```
web/templates/topic/show.html.eex
```
This is the page you get when you click the "Show" link on the "Listing topics" page.

```
web/templates/topic/new.html.eex
```
This is the page you get when you click "New Topic".

```
web/templates/topic/edit.html.eex
```
This is the page you get when you click "Edit".

```
web/templates/topic/form.html.eex
```
You may have noticed that the page for new topics and the page to edit topics looked similar. That's because they both use the code from this file to show a form. This file is called a partial since it only contains code for part of a page. Partials always have filenames starting with an underscore character.
Challenge question: Can you find the line of code in new.html.eex and edit.html.eex that makes the form partial appear?

```
web/controllers/topics_controller.ex
```
This is the controller file that Phoenix created as part of the scaffold
If you look you'll see a method (a line beginning with def) for each of the views listed above (except form.html.eex)
