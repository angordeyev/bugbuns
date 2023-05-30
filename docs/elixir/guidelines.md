## Guidelines

## Links

[The Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide)
[Library Guidelines[^1]](https://hexdocs.pm/elixir/1.13/library-guidelines.html#getting-started)

## Repository and Packages Naming

Use snakecase

## Example

    # One space after after "#" is used in comments.
    # Comments longer than a word are capitalized, and sentences use punctuation.
    # Modules use Camel case and keep acronyms (snake case does
    # not save acronyms, e.g. "parse_html").
    defmodule MyModuleHTML do
      @moduledoc """
      An example module.
      Blank line after module documentation.
      """

      @behaviour MyBehaviour

      use GenServer

      import Something
      import SomethingElse

      require Integer

      alias My.Long.Module.Name
      alias My.Other.Module.Example

      @module_attribute :foo
      @other_attribute 100

      defstruct [:name, params: []]

      @type params :: [{binary, binary}]

      @callback some_function(term) :: :ok | {:error, term}

      @macrocallback macro_name(term) :: Macro.t()

      @optional_callbacks macro_name: 1

      @doc false
      defmacro __using__(_opts), do: :no_op

      @doc """
      Determines when a term is `:ok`. Allowed in guards.
      """
      defguard is_ok(term) when term == :ok

      @impl true
      def init(state), do: {:ok, state}

      # Define other functions here.
      # Use blank lines even for overloaded functions
      # Group one line functions without blank line

      # Omit parentheses when there are no function arguments
      def some_overloaded_function, do: :ok
      def some_overloaded_function(1), do: 1

      # blank line before function, multiline function,
      # same as def..end function
      def some_overloaded_function(_),
        do: :very_long_line_here

      # opts is the name for options parameters
      def some_overloaded_function(:ok, opts \\ :default_value) do
        # Blank line before and after multiline assignment
        some_var = 1

        something =
          if x == some_var do
            "Hi"
          else
            "Bye"
          end

        String.downcase(something)

        # Place begining and "end)" with the same indentation
        spawn(fn ->
          Logger.debug("three")
          send(test, :done)
        end)
      end

      @doc """
      Docs are written for a first overloaded function.
      """
      def some_overloaded_function(some_string) do
        # Blank line between each of case statement
        case arg do
          true ->
            # comments above, not after line
            IO.puts("ok")
            :ok

          false ->
            :error
        end

        # Blank line between commented one line statements

        # Some comment
        a = 1

        # Another comment
        b = 1

        # Pipeline, lines are not indented
        some_string
        |> String.downcase()
        |> String.trim()

        # Assignment and pipeline
        some_result =
          some_string
          |> String.downcase()
          |> String.trim()

        # Heredoc, leading spaces are removed according to the last """
        text = """
        some
        text
        """

        assert text == """
               some
               text
               """
      end

      # acronym in lower case in snake case
      def parse_json(text) do
        ..
        some_fun = fun x ->
          ...
        end

      end

      def multiline_lists_and_tuples do
        # list assignment
        list = [
          :first_item,
          :second_item
        ]

        # tuple assignment
        tuple = {
          :first_item,
          :second_item
        }

        # return list
        [
          :first_item,
          :second_item,
          :next_item,
          :final_item
        ]

        # return tuple
        {
          :first_item,
          :second_item,
          :next_item,
          :final_item
        }
      end

      def multiline_maps do
        # map assignment
        map = %{
          "first_key" => "first_value",
          "second_key" => "second_value"
        }

        # return map
        %{
          "first_key" => "first_value",
          "second_key" => "second_value"
        }
      end

      def function_with_long_parameters(%{
            label: {GenServer, :no_handle_info},
            report: %{module: mod, message: msg, name: proc}
          }) do
        {'~p ~p received unexpected message in handle_info/2: ~p~n', [mod, proc, msg]}
      end

      def pattern_matching_function([:foo, :bar, :baz] = params),
        do: Enum.map(args, fn arg -> arg <> " is on a very long line!" end)
    end

    # no blank line after defmodule and before end
    defmodule A do
      def f, do: :ok
    end

<!---->

    defmodule MyModuleHTMLTest do
      use Simple.DataCase

      ...
    end

## Blank lines

> Add a blank line between each grouping, and sort the terms (like module names) alphabetically.

## Definition order

The order in a module:

"Use Ira"

- use
- import
- require
- alias

## text wrap

    list = [
      :first_item,
      :second_item
    ]

    sanitized_string =
      some_string
      |> String.downcase()
      |> String.trim()

## get[^2] fetch[^3] and bang(!)

    dict = %{a: 1, b: 2}

    Map.get(dict, :a) # 1
    Map.get(dict, :c) # nill, default value
    Map.get(dict, :c, 3) # 3, default value

    # Getting by `[index]` have the same behaviour as Map.get function
    dict[:a] # 1
    dict[:c] # nil

    Map.fetch(dict, :a) # {:ok, 1}
    Map.fetch(dict, :c) # :error

    Map.fetch!(dict, :a) # 1
    Map.fetch!(dict, :c) # (KeyError) key :c not found in: %{a: 1, b: 2}

Application has the same naming pattern for get_env:

    Applicaton.get_env/2
    Applicaton.fetch_env!/2
    Applicaton.fetch_env/2

## Resources

[^1]: методические рекомендации
[^2]: "получить"
[^3]: fetch means "go and get" something, "принести, забрать"
