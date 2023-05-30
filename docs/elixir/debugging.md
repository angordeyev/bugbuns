## Debugging

### Inspecting

    [1, 2, 3]
    |> IO.inspect() # prints [1, 2, 3]

Using inspect label in pipelines

    [1, 2, 3]
    |> IO.inspect(label: "before") # prints "before: [1, 2, 3]"
    |> Enum.count() # retuns 3

### Pry

use `IEX.pry`[^2]

    a = "hello"
    IO.puts a # a
    # interactive shell will ask to stop here,
    # press "n" to continue or "y" to debug
    require IEx; IEx.pry()

In pry mode

    pry> IO.puts a # hello

### Breakpoints

### Debug in tests

`mix test` does not work, use `iex -S mix` instead

### Observer

    :observer.start

### Tools

[Recon](https://hex.pm/packages/recon)

    :recon_trace.calls({Phoenix.Socket.Transport, :check_origin, :return_trace}, 1000)

### Resources

[Debugging with Tracing in Elixir with recon_trace](https://github.com/kw7oe/livebook-notebooks/blob/main/debugging-with-tracing-in-elixir-with-recon_trace.livemd)
[Debugging With Tracing in Elixir](https://kaiwern.com/posts/2020/11/02/debugging-with-tracing-in-elixir/#starting-dbg)
[Debugging techniques in Elixir. Plataformatec.](http://blog.plataformatec.com.br/2016/04/debugging-techniques-in-elixir-lang/)
[Tracing and observing your remote node. Plataformatec.](http://blog.plataformatec.com.br/2016/05/tracing-and-observing-your-remote-node/)
[Stuff Goes Bad ERLANG IN ANGER, Fred Hebert](https://www.erlang-in-anger.com/)
[ElixirConf 2020 - Jeffery Utter - Debugging Live Systems on the BEAM](https://youtube.com/watch?v=sR9h3DZAA74)
[Debugging Elixir Code: The Definitive Guide](https://curiosum.com/blog/debugging-elixir-code-the-definitive-guide)
[Debugging Elixir Code - The Tools, The Mindset | Michal Buszkiewicz | ElixirConf EU 2021]([https://www.youtube.com/watch?v=x9OMlrrKYyE)
[Elixir Remote Debugging. Codemancers.](https://crypt.codemancers.com/posts/2017-11-22-elixir-remote-debugging/)
https://mfeckie.github.io/Remote-Profiling-Elixir-Over-SSH/
