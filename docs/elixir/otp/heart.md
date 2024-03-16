# Heart

```shell
elixir --erl "-heart" -e "Enum.map Stream.interval(1000), &IO.puts/1"
```

```shell
export HEART_COMMAND="run_erl -daemon ./my_app ./log \"MIX_ENV=prod iex --erl '-heart +K true +A 16' -S mix run --no-halt --no-compile --no-deps-check\""
```
