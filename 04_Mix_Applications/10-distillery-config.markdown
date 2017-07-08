## Distillery Config

Next we will set up our config for distillery.  Let'e open up our `rel` directory that we created when we ran the `mix release.init` command. 

Delete what is currently in that file and paste in the code below. 

```elixir
use Mix.Releases.Config,
  default_release: :default,
  default_environment: Mix.env
environment :dev do
  set dev_mode: true 
  set include_erts: false
  set include_system_libs: false
  set cookie: :dev
end
environment :prod do
  set include_erts: true
  set include_system_libs: true
  set cookie: :prod
end
release :myapp do
  set version: current_version(:myapp)
end
```


