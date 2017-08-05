---
layout: page
title: Multi-Room chat
date: 2016-08-04 23:08:17 -0700
position: 3
---

## Adding rooms

In this section, we'll add the concept of separate rooms to our app, along with the idea of accounts (which for now are disposable, with no auth). Let's get started implementing.

First, let's generate our new schemas:

```bash
mix phx.gen.schema Room rooms room_name:string
mix phx.gen.schema Account accounts name:string
mix phx.gen.schema AccountRoom account_rooms account_id:references:accounts room_id:references:rooms
```

After we generate these, we'll want to add columns to the `Message` schema so that it references the `room_id` and `account_id`.

```bash
mix ecto.gen.migration add_room_and_account_to_message
```

