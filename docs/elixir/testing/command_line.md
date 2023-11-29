# Commands

## Help

```shell
mix help test
```

## Run Tests in Interactive Mode

```shell
iex -S mix test
```

## List Tests

Run with `--trace` options and see tests listed in green

```shell
mix test --trace
```

## Filter Tests

### Work in Progress

To mark single test use `@tag :wip`, it is equivalent of `@tag wip: true`

```elixir
@tag :wip
test "sometest" do
  #...
end
```

Or an entire module:

```elixir
def SomeTestModule do
  ...
  @moduletag :wip
  ...
end
```

Run tagged test:

```shell
mix test --only wip
```

### Filter Tests in Files

Run tests in a file:

```shell
mix test path/to/test/some_test.exs
```

Run tests using a path and a line:

```shell
mix test path/to/test/come_test.exs:10
```

### Filter Using Describe Section

`describe` can be used as a tag to filter tests to run:

```shell
mix test --only describe:"described test"
````

Or to list tests, filtered tests will be shown in green text:

```shell
mix test --trace --only describe:"described test"
```

### Print Slowest Tests

```shell
mix test --slowest <n>
```
