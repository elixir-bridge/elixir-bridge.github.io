---
layout: post
title: Allow users to vote on topics
date: 2016-08-28 15:17:10 -0700
position: 12
---

# Goals
Now we're going to add a button people can click to cast a vote.

## Steps
### Step 1: Add a new controller action for voting
Edit web/controllers/topic_controller.ex and add this method at the end of the controller, above the last `end` keyword:
```
def upvote(conn, %{"topic_id" => id}) do
  TestApp.Vote.changeset(%TestApp.Vote{}, %{topic_id: id})
    |> TestApp.Repo.insert
  conn
    |> put_flash(:info, "Upvoted!")
    |> redirect(to: topic_path(conn, :index))
end
```
If the first part of this code looks familiar, it's because it is almost the same as the code we used to add a vote in the console, just with a newline before the pipe operator for readability. We take the id of the topic we'd like to upvote and add a vote to the database with it included. Then, we set a message to be displayed, and redirect the request back to the index action.

### Step 2: Add a new route for voting
Open web/router.ex and find the section that looks like this:

```
scope "/", TestApp do
  pipe_through :browser # Use the default browser stack

  resources "/topics", TopicController
  get "/", TopicController, :index
end
```

Replace the `resources "/topics"` line with the following:
```
resources "/topics", TopicController do
  post "/upvote", TopicController, :upvote
end
```

Verify that upvote route was added successfully by checking the output of `mix phoenix.routes`. You should see a line that looks like this:
```
      Prefix Verb   URI Pattern                  Controller#Action
topic_topic_path  POST    /topics/:topic_id/upvote  TestApp.TopicController :upvote
```

### Step 3: Add the button to the view
Edit `web/templates/topic/index.html.eex` so that the bottom loop looks like this:

```
<%= for topic <- @topics do %>
    <tr>
      <td><%= topic.description %></td>
      <td><%= topic.title %></td>    
      <td><%= count(topic.votes) %> <%= ngettext("vote", "votes", count(topic.votes)) %></td>

      <td class="text-right">
        <%= link "Show", to: topic_path(@conn, :show, topic), class: "btn btn-default btn-xs" %>
        <%= link "Edit", to: topic_path(@conn, :edit, topic), class: "btn btn-default btn-xs" %>
        <%= link "+1", to: topic_topic_path(@conn, :upvote, topic), method: :post, class: "btn btn-default btn-xs" %>
        <%= link "Delete", to: topic_path(@conn, :delete, topic), method: :delete, data: [confirm: "Are you sure?"], class: "btn btn-danger btn-xs" %>
      </td>
    </tr>
<% end %>
```

You'll also need to modify the index action in the controller to load the votes:

```
def index(conn, _params) do
  query = from t in Topic, preload: :votes
  topics = Repo.all(query)
  render(conn, "index.html", topics: topics)
end
```

The substantive difference here is `preload: :votes`, which makes the database get the votes that belong to each topic, in the same query that gets the votes.
`ngettext("vote", "votes", count(topic.votes))` displays the number of votes the topic has, plus the word "vote" or "votes" accordingly.
`link "+1", to: topic_topic_path(@conn, :upvote, topic)` creates an HTML button with the text "+1".
`topic_topic_path(topic)` creates the appropriate URL for the action we want to invoke. In this case, we want to upvote the current topic. `topic_topic_path(topic)` returns `/topics/42/upvote` (if topic.id was 42).
`method: :post` ensures we do the create action of CRUD, not the read action.

### Step 4: Confirm your changes in the browser
Go back to http://localhost:4000/topics and play.

Revel in the fact that you didn't have to restart the server to see these changes.

## Deploying
Before the next step, you could try deploying your app to Heroku!

If you have already deployed your app to Heroku, go on to Deploying to Heroku again.
If this is your first time deploying your app, start at Deploying to Heroku

Next Step:
Go on to [TODO: FILL ME IN WHEN LAST LESSONS ARE DONE](/index.html)

Back to [Joining Votes And Topics](11-joining-votes-and-topics.html)
