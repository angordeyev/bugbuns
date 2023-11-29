# Tests

## Sections

### setup_all

`setup_all` runs once for a test module:

```elixir
setup_all do
  # setup code
end
```

### setup

setup runs for each test.

```elixir
setup do
  # setup code
end
```

`setup` and `setup_all` sections cannot be defined inside `describe` block.

### describe

Describe adds prefix name to tests and allow to define common setup section for tests.

Add setup section to `describe"` section:

```elixir
describe "index" do
  setup %{conn: conn} do
    {:ok, conn: put_req_header(conn, "some_key", "some_value")}
  end
  ...
end
```

Add pry to the controller:

```elixir
def index(conn, _params) do
  require IEx; IEx.pry()
  ...
end
```

See the request headers

```elixir
iex> conn.req_headers
```
```output
[{"accept", "application/json"}, {"some_key", "some_value"}]
```

Do the same for `UserController.show/2` function (add `pry` and run tests).

See the request headers:

```elixir
iex> conn.req_headers
```
```output
[{"accept", "application/json"}]
```

## Asserts

### Assert with Pattern Matching

```eliir
assert %{a: 1, b: bb} = %{a: 1, b: 22, c: 33}
```

## Run Group of Tests on Demand

We can tag group of tests to run only if specific parameter is passed on the command line. One of the examples is to run integration tests.

Configure ExUnit to exclude tests with a particular tag by adding to `test_helper.exs`:

```elixir
ExUnit.configure(exclude: [external: true])
```

Mark tests with a tag:

```elixir
@tag external
test "some test" do
  ...
end
```

Or mark description sections

```elixir
@tag :external
describe "some section" do
  test "some test" do
    ...
  end
  ...
end
```

Then we can run excluded tests only

```shell
mix test --only external
```

Or all project tests

```shell
mix test --include external
```

## Debugging

To execute code inside test use

```elixir
require IEx; IEx.pry()
```

## Livebook

To write tests in livebook see [Livebook](../livebook/livebook.md)
