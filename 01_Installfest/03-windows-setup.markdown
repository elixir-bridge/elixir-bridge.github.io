---
layout: page
title: Windows setup
date: 2019-04-25 02:55:28 -0500
---

## Windows

### Step 1: Download Elixir Windows installer

[Elixir Windows installer download](https://elixir-lang.org/install.html#windows)

- Choose Elixir version 1.8.1
- Install Erlang / 64-bit
- Follow installer instructions
  - Erlang will be downloaded
- Complete Erlang installation
  - Elixir will be downloaded
- Complete Elixir installation
- Reload all terminal windows (if any)
- Test that erlang and elixir work

As an alternative, you can use Chocolatey to install Elixir:

#### Chocolatey installation

Navigate to [https://chocolatey.org/install](https://chocolatey.org/install).

Install the chocolatey package.

Then install elixir. Follow the instructions here: [https://chocolatey.org/packages/Elixir](https://chocolatey.org/packages/Elixir)

#### Verify elixir installation

```
elixir -v
```

Expected result:

```
Erlang/OTP 21 [erts-10.1] [64-bit] [smp:12:12] [ds:12:12:10] [async-threads:1]

Elixir 1.8.1 (compiled with Erlang/OTP 20)
```

### Step 2: Install Postgresql

[Postgres Windows Installer](https://www.postgresql.org/download/windows/)

- To modify your environment variables, first open up Control Panel
- Search for "environment"
- Click `Edit environment variables for your account`
- Click the Path variable, then Edit
- Add the path to the Postgres bin folder

* Depending on your install it could be in C:\Program Files\PostgreSQL\11\bin

```
psql -U postgres
```

Expected result:

```
Password for user postgres:
psql (11.2)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=#
```
