## do block

`do <block> end` is syntax sugar for `do: <block>`

    iex> IO.inspect(do: true)
    [do: true]
    [do: true]

    iex> IO.inspect do true end
    [do: true]
    [do: true]

    iex> IO.inspect do IO.puts("hi") end
    hi
    [do: :ok]
    [do: :ok]

    defmodule Args do
      def get_arg(arg) do
        binding()
      end

      def get_args(arg1, arg2) do
        binding()
      end
    end

    iex> Args.get_arg(true)
    [arg: true]

    iex> Args.get_arg true
    [arg: true]

    iex> Args.get_arg(do: true)
    [arg: [do: true]]

    iex> Args.get_arg do true end
    [arg: [do: true]]

    iex> Args.get_args(1, 2)
    [arg1: 1, arg2: 2]

    iex> Args.get_args(1, do: 2)
    [arg1: 1, arg2: [do: 2]]

    iex> Args.get_args 1, do: 2
    [arg1: 1, arg2: [do: 2]]

    iex> Args.get_args 1 do 2 end
    [arg1: 1, arg2: [do: 2]]

    iex> Args.get_args do 1 end 2 # do end should go last
    (SyntaxError) iex:20:24: syntax error before: "2"

    iex> Args.get_args 1 do 2 else 3 end
    [arg1: 1, arg2: [do: 2, else: 3]]


    defmodule ArgsCode do
      defmacro get_arg(arg) do
        IO.inspect(arg)
        :ok
      end

      defmacro get_args(arg1, arg2) do
        IO.inspect(arg1, label: "arg1")
        IO.inspect(arg2, label: "arg2")
        :ok
      end
    end

    iex> require ArgsCode
    iex> ArgsCode.get_arg(true)
    true
    :ok

    iex> ArgsCode.get_arg do: true
    [do: true]
    :ok

    iex> ArgsCode.get_arg do true end
    [do: true]
    :ok

    iex> ArgsCode.get_args 1, do: 2
    arg1: 1
    arg2: [do: 2]
    :ok

    iex> ArgsCode.get_args 1 do 2 end
    arg1: 1
    arg2: [do: 2]
    :ok

