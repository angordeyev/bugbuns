# Profiling

```elixir
Mix.install([{:exprof, "~> 0.2.4"}])
```
## Code

```elixir
import ExProf.Macro

profile do
  Process.sleep(100)
  IO.puts("hi")
end
```

## Resources

* [Profiling Elixir. Joseph Kain.](http://learningelixir.joekain.com/profiling-elixir/)
* [Profiling a Slow Elixir Test. Bryan Stearns.](https://selfamusementpark.com/coding/profiling-a-slow-elixir-test)
