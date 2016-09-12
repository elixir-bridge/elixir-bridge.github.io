---
layout: post
title: Clean Up Topics List
date: 2016-09-07 20:23:39 -0700
---

## Goals
Our app is nearly done! The main topics listing page is pretty busy. There are a lot of links that aren't necessary.

Let's clean up the topics list page by doing the following:

* Remove the 'show' link
* Remove the 'edit' link
* Change 'destroy' to 'delete'

### Steps
#### Step 1: Remove the 'show' and 'edit' links
Open `test_app/web/templates/topic/index.html.eex` and remove these two lines:

```
<%= link "Show", to: topic_path(@conn, :show, topic), class: "btn btn-default btn-xs" %>
<%= link "Edit", to: topic_path(@conn, :edit, topic), class: "btn btn-default btn-xs" %>
```

Step 2: Change 'Delete' to 'Remove'
Change the line with the word 'Destroy' to this:
```
<%= link "Remove", to: topic_path(@conn, :delete, topic), method: :delete, data: [confirm: "Are you sure?"], class: "btn btn-danger btn-xs" %>
```
## Explanation
* The two links we removed were show and edit. We did this because the title now links to the show page and from the show page you can reach the edit page.

* The second change we made was to make the link text 'Delete' instead of 'Destroy'.

## Deploying
Before the next step, you could try deploying your app to Heroku!

* If you have already deployed your app to Heroku, go on to Deploying to Heroku again.
* If this is your first time deploying your app, start at Deploying to Heroku

## Next Step:
Go on to Credits And Next Steps
