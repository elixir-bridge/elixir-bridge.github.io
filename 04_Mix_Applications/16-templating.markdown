## Templating

Elixir allows you to create template files to create views for your web application. EEX stands for embedded elixir and it works like ERB for Ruby or Jinja for Python.


```elixir
get "/" do
  page = EEx.eval_file("templates/home.html")
  conn
    |> put_resp_content_type("text/html")
    |> send_resp(200, page)
    |> halt
end
```

As we can see above, the `eval_file/3` allows us to retrieve a file name, and evaluate the values using bindings. 

We can then send that template back in a response to the client. 

### Interpolation

In Eex we can interpolate variables list so:

```elixir
<h2><% name %></h2>
```