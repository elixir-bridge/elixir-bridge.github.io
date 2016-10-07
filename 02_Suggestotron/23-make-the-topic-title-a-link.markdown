---
layout: page
title: Make the Topic title a Link
date: 2016-08-28 15:17:10 -0700
position: 13
---

# Goals
Your friends recommended two changes for the site:

* Don't show the description on the list page

* Make the title a link and when it's clicked show the description

## Steps

### Step 1: Remove the description
Let's start by removing the description. Open ` web/templates/topic/index.html.eex` and delete the line that looks like this:

```
<td><%= topic.description %></td>
```

Also delete the line that looks like this:

```
<th>Description</th>
```

If you save and try to load it in the browser you should see that the description no longer appears.

### Step 2: Make the title a link
Now make the title a link by editing app/views/topics/index.html.erb (again) and replacing this line:

```
<td><%= topic.title %></td>
```
with this:

```
<td><%= link topic.title, to: topic_path(@conn, :show, topic), method: :get %></td>
```

## Explanation
```
<td><%= topic.description %></td>
```
This line was getting the description using .description and just printing it out.

```
<th>Description</th>
```

`<th>` stands for table header and everything between <th> and </th> was being printed as a table header (bold). We removed it since we removed the description and it would look funny to have the header and the wrong thing below it.

```
<td><%= link topic.title, to: topic_path(@conn, :show, topic), method: :get %></td>
```
Here's another use of `link/2` to create a link on the page. This `link` creates a link using the text from the topic title and goes to the topic show page.
