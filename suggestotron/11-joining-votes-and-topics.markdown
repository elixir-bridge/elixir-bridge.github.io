---
layout: page
title: Joining Votes and topics
date: 2016-08-28 12:49:19 -0700
position: 11
---

# Hooking Up Votes And Topics

## Goals

|Topics|
|id|
|title|
|description|


|Votes|
|id|
|topic_id|

Because there is an explicit relationship between a topic and its votes, we need to specify that. In this step, we'll explicitly declare the relationship between votes and topics.

# Steps
## Step 1: Teach the Topic model about Votes
Open the file `web/models/topic.ex`, and add a line after `timestamps` that says `has_many :votes, TestApp.Vote`. That section of code should look like this when you're done:

```
schema "topics" do
  field :description, :string
  field :title, :string

  timestamps

  has_many :votes, TestApp.Vote, on_delete: :delete_all
end
```

## Step 2: Teach the Vote model about Topics
Edit the schema block of `web/models/vote.ex` so that it looks like this:

```
  schema "votes" do
    timestamps
    belongs_to :topic, TestApp
  end
```

## Step 3: Play around with Topics and Votes in `iex`

First, make sure you've made at least one topic on the site.

Next, open an iex console in a terminal window:
```
iex -S mix
```
Expected result:
```
iex -S mix
Erlang/OTP 18 [erts-7.3] [source] [64-bit] [smp:4:4] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]
Compiled web/models/topic.ex
Compiled web/models/vote.ex
Compiled web/controllers/topic_controller.ex
Interactive Elixir (1.2.4) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```
The lines that start with `Compiled` may be different in your output.

At the console, try the following things

See how many topics exist:  
```
iex(1)> TestApp.Repo.aggregate(TestApp.Topic, :count, :id)
[debug] QUERY OK db=8.1ms queue=2.2ms
SELECT count(t0."id") FROM "topics" AS t0 []
1
```

Save the first topic into a variable:
```
my_topic = TestApp.Repo.one(TestApp.Topic)
```
my_topic here could have been any variable name, but we'll stick with my_topic for consistency.

Change the title of that topic to something else:
```
TestApp.Topic.changeset(my_topic, %{title: "Edited in the console"}) |> TestApp.Repo.update
```
Here we've introduced a powerful bit of syntax, the `|>`, or pipe operator. It takes the output of the preceding command and sends it to the next command. Here, you create a changeset, or a list of the changes you'd like to make in the first half of the line, and then the second half, sent those changes to the database.

Add a vote to that topic:
```
TestApp.Vote.changeset(%TestApp.Vote{}, %{topic_id: my_topic.id}) |> TestApp.Repo.insert
```

Here, we create a `Vote` changeset, and since we're creating it, we initalize it with `%TestApp.Vote{}`, and add the topic id. Then, we pipe that to the database with `TestApp.Repo.insert`.

See how many votes that topic has:

```
iex(6)> my_topic = my_topic |> TestApp.Repo.preload(:votes)
iex(7)> my_topic.votes |> length
```

Remove a vote from that topic:

```
[vote | _rest] = my_topic.votes
Repo.delete!(vote)
```



Explanation
has_many and belongs_to:

In Phoenix, relationships between models are called associations.
Associations (usually) come in pairs.
A topic will have many votes so we put `has_many :votes` in the topic model.
When you ask a topic for its votes, you get a list of votes for that topic.
A vote is for a particular topic, so we put `belongs_to :topic` in the vote model.
When you ask a vote for its topic, you get the topic for that vote.
It can still be important to clean up after yourself! `on_delete: :delete_all` on `has_many :votes` means when a Topic gets destroyed, all the votes that correspond to it will be destroyed, too. Without dependent :destroy, those votes would live on the database forever.

Next Step:

## Next Step
Go on to [Allow People To Vote](/suggestotron/12-allow-users-to-vote-on-topics.html)
or,
Go Back to [Voting On Topics](/suggestotron/10-voting-on-topics.html)
