---
layout: page
title: Generate a Database Model
date: 2016-09-24 12:28:28 -0700
---

#### Step 7 : Generate a database model

Phoenix gives us a phoenix.gen.schema task similar to Rails `rails generate scaffold`



Now that the database has been created with `mix ecto.create`, type this into the terminal:

```
mix phoenix.gen.schema Drink drinks name:string temperature:string
```

You should see output similar to this:

```
* creating web/controllers/drink_controller.ex
* creating web/templates/drink/edit.html.eex
* creating web/templates/drink/form.html.eex
* creating web/templates/drink/index.html.eex
* creating web/templates/drink/new.html.eex
* creating web/templates/drink/show.html.eex
* creating web/views/drink_view.ex
* creating test/controllers/drink_controller_test.exs
* creating web/models/drink.ex
* creating test/models/drink_test.exs
* creating priv/repo/migrations/20160828191433_create_drink.exs

Add the resource to your browser scope in web/router.ex:

    resources "/drinks", DrinkController

Remember to update your repository by running migrations:

    mix ecto.migrate
```

Now let's follow the instructions at the end of that output.

We'll add routes. Open up a file named `lib/test_app_web/router.ex`

Around line 19 (this will vary depending on your editor) delete the section that looks like

```
 scope "/", TestApp do
    pipe_through :browser # Use the default browser stack

    get "/", PageController, :index

    resources "/pages", PageController
  end
```
and paste in the following

```
scope "/", TestApp do
    pipe_through :browser # Use the default browser stack

    get "/", DrinkController, :index

    resources "/drinks", DrinkController
  end
```

Now type this into the terminal

```
mix ecto.migrate
```

You will see something similar to the following on your screen

![phoenix datbase migration output](/assets/phoenix-db-migration-output.png)

Now lets start our server up again

Type the following into the terminal

```
mix phx.server
```

Then go to your browsers and type in
localhost:4000

You should see a page that looks something like this

!['test app image'](/assets/test-app-index.png)


Wait till your server has loaded like before.

Then in the browser url bar type in:
```
http://localhost:4000/drinks
```

1) Click on new drink

2) Enter Cappuccino for the name

3) Enter 135 for the temperature.

4) Click on "Create Drink".

You should see the following text at the top of the page

![drinks successfully created ](/assets/drinks-created.png)
