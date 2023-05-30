## mix.exs versions

If you upgraded to the next version, then reverted and get errors, `git checkout mix.lock` and rebuild, it may help. Checkout will revert previosuly locked versions of components.

## inets
In case of inets error after Phoenix release

    (MatchError) no match of right hand side value: {:error, {:inets, {'no such file or directory', 'inets.app'}}}

Add `inets` to `extra_applications` in `mix.exs`

    def application do
      [
        ...
        extra_applications: [:logger, :runtime_tools, :inets]
        ...
      ]
    end

## Conditional compilation

    defmodule HelloConditional do
      if Mix.env() in [:dev, :test] do
        def hello_dev do
          "hello dev"
        end
      end

      if Mix.env() == :prod do
        def hello_dev do
          "hello prod"
        end
      end
    end

    ➜ MIX_ENV=dev iex -S mix

    iex> HelloConditional.hello_dev()
    "hello_dev"

    iex> HelloConditional.hello_prod()
    (UndefinedFunctionError) function HelloConditional.hello_prod/0 is undefined

    ➜ MIX_ENV=prod iex -S mix

    iex> HelloConditional.hello_prod()
    "hello_prod"

    iex> HelloConditional.hello_dev()
    (UndefinedFunctionError) function HelloConditional.hello_dev/0 is undefined

## Compile-time code

    # HelloCompileTime.ex
    IO.puts("out of module")
    defmodule HelloCompileTime do
      IO.puts("in module")
    end

    ➜ mix compile
    out of module
    in module

    ➜ iex -S mix # no messages
