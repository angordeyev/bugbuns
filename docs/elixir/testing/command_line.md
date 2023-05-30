# Commands

## Help

    ➜ mix help test

## Run Tests in Interactive Mode

    ➜ iex -S mix test

## List Tests

Run with `--trace` options and see tests listed in green

    ➜ mix test --trace

## Filter Tests

### Work in Progress

To mark single test use `@tag :wip`, it is equivalent of `@tag wip: true`

    @tag :wip
    test "sometest" do
      #...
    end

Or an entire module

    def SomeTestModule do
      ...
      @moduletag :wip
      ...
    end

Run tagged test

    ➜ mix test --only wip

### Filter Tests in Files

Run tests in a file

    ➜ mix test path/to/test/some_test.exs

Run tests using path and line

    ➜ mix test path/to/test/come_test.exs:10

### Filter Using Describe Section

Describe can be used as tag to filter tests to run

    ➜ mix test --only describe:"described test"

Or to list tests, filtered tests will be shown in green text

    ➜ mix test --trace --only describe:"described test"
