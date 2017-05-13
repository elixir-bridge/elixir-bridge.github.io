---
layout: page
title: Deploy to Heroku
date: 2016-09-24 12:28:28 -0700
---

### Deploy Time!!!

Go to heroku.com

Click on your app

Click on Resources

You should see something like

![heroku dashboard](/assets/heroku-dashboard-resources.png)

At the serach bar near the bottom of the page type in `postgres`

You should see a pop up menu, select the option for `Heroku Postgres`

You will see the following window pop up

![heroku provision postgres](/assets/provision-heroku-postgres.png)

Click on `Provision`


Then Click on settings


![heroku app interface](/assets/heroku-app-interface.png)

You should see something that looks like this

![heroku config vars](/assets/reveal-heroku-config-vars.png)

Click on the button that says **Reveal Config Vars**

Make sure you have the following environment variables set.
Note - they may not be set in this same order. Anything not
in this list, you should set.

```yaml
DATABASE_URL: heroku-sets-this-for=you
DATABASE: heroku-sets-this-for=you
MIX_ENV: prod  **you need to set this one**
PASSWORD: heroku-sets-this-for=you
POOL_SIZE: 18
SECRET_KEY_BASE:
USER_NAME:
```

Now in the empty row at the bottom of the page

![empty heroku config var](/assets/empty-heroku-config-var1.png)

in the first empty field create a new variabel called

'NEW_DATABASE_URL'

Then take a look at your database url, but clicking on the pencil icon next to it. It should look something like

```shell
postgres://xxxxxxxxxxxxxxx@xxxxxxxxx.amazonaws.com:5432/xxxxxxx
```

Copy the portion after the @ sign through amazon.com and paste it as the value for the NEW_DATABASE_URL

so it will be something like `abedsd.amazonaws.com.

Then in the next blank field under the var settings type in `USERNAME' on the right. Then take another look at your database url.

for example this database url look like so

```html
postgres://abscdefg:123456.compute-1.amazonaws.com:5432/d51oep5q7b7bbi
```
It has the following format

```html
postgres://username:password.compute-1.amazonaws.com:5432/databse
```

Copy the username portion of the url and paste is at teh left value in your config variables.

Then Click Add.

It should look like this

![heroku-database-username](/assets/heroku-db-username.png)

Do the same for password. Create a Variable called password. and then cpy the password from the correct portion of the database url
```
postgres://username:password.compute-1.amazonaws.com:5432/databse
```

Do the same again for database. Create a Variable called `DATABASE` and copy the value from the end of the database to set as the value/


Your config should look something like this
![heroku config](/assets/heroku-config1.png)



You should have the following variables now defined

```yaml
DATABASE_URL:
DATABASE:
MIX_ENV:
PASSWORD:
POOL_SIZE:
SECRET_KEY_BASE:
USER_NAME:
NEW_DATABSE_URL:
```

Then Open up your `config/prod.exs` file, and change the value of the host name so it is using the NEW_DATABASE_URL -

It should look like this

```elixir
# Configure your database
config :test_app, TestApp.Repo,
  adapter: Ecto.Adapters.Postgres,
  hostname: System.get_env("NEW_DATABASE_URL"),
  pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
  ssl: true,
  database: System.get_env("DATABASE"),
  username: System.get_env("USERNAME"),
  password: System.get_env("PASSWORD")
```
Let's commit all our changes. Copy each of the lines below into your terminal one at a time. Do not do this all at once.

```bash
git add config/prod.exs
git add Procfile.txt
git add web/channels/user_socket.ex
git commit -m "Use production config from Heroku ENV variables and deploy environment"
```

And now DEPLOY!!

Type this into your terminal:

```bash
git push heroku master
```

You will see a bunch of stuff and at the end you will see

```bash
remote:
remote: Verifying deploy.... done.
To https://git.heroku.com/stormy-stream-65433.git
   ae7601a..e5c410b  master -> master
Annas-MacBook-Pro-3:test_app anheroku logs -a stormy-stream-65433
```

You do not see the 'Verifying deploy...done', ask a TA for help.


next type the following into your terminal

```bash
npm install brunch
```

then type

```bash
node_modules/brunch/bin/brunch  build --production

```

finally type



```bash
heroku run "mix ecto.migrate"
```

YAY all done!

Type

```bash
heroku open
```
to see your app.
