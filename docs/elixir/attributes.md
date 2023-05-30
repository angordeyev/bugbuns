## Module Attributes

### Simple Project

Module attributes are compile time

Generate the new project

    ➜ mix new hello_attributes

Add attribute to the module

    @some_attribe IO.puts("hi")

    def hello do
      @some_attribe
    end

Compile and see "hi" message

    ➜ mix compile --force
    Compiling 1 file (.ex)
    hi
    Generated hello_attributes app

Run

    ➜ rm -rf _build # remove builded files
    ➜ iex -S mix
    Compiling 1 file (.ex)
    hi
    Generated hello_attributes app

    iex> HelloAttributes.hello()
    :ok

### Module Attributes

Attributes are compile time and are used as constants

    defmodule OtherModule do
      def some_const() do
        IO.puts "hello"
        "world"
      end
    end

    defmodule MyModule do
      @my_const OtherModule.some_const()

      def hello do
        IO.puts @my_const # world
      end
    end

"hello" is shown at compile time

    Compiling 1 file (.ex)
    hello
    Generated hello_docs app
    Interactive Elixir (1.13.4) - press Ctrl+C to exit (type h() ENTER for help)
    iex(1)>

"world" is is shown at runtime

    iex> MyModule.hello
    world
    :ok

Or annotations

    defmodule HelloWorld do
      @moduledoc """
      Interaction with the world
      """

      @doc """
      Prints "hello world"
      """
      def hello() do
      end
    end

    iex> h HelloWorld # Interaction with the world
    iex> h HelloWorld.hello # Prints "hello world"
