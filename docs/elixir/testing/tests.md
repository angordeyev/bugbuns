# Tests

## Sections

### setup_all

setup_all runs once for a test module.

    setup_all do
      # setup code
    end

### setup

setup runs for each test.

    setup do
      # setup code
    end

`setup` and `setup_all` sections cannot be defined inside `describe` block.

### describe

Describe adds prefix name to tests and allow to define common setup section for tests.

Add setup section to "describe" section

    describe "index" do
      setup %{conn: conn} do
        {:ok, conn: put_req_header(conn, "some_key", "some_value")}
      end
      ...
    end

Add pry to controller

    def index(conn, _params) do
      require IEx; IEx.pry()
      ...
    end

See request headers

    iex> conn.req_headers
    [{"accept", "application/json"}, {"some_key", "some_value"}]

Do the same for `UserController.show/2` function (add `pry` and run tests).

See request headers

    iex> conn.req_headers
    [{"accept", "application/json"}]

## Asserts

### Assert with Pattern Matching

    assert %{a: 1, b: bb} = %{a: 1, b: 22, c: 33}

## Run Group of Tests on Demand

We can tag group of tests to run only if specific parameter is passed on the command line. One of the examples is to run integration tests.

Configure ExUnit to exclude tests with a particular tag by adding to `test_helper.exs`

    ➜ ExUnit.configure(exclude: [external: true])

Mark tests with tag

    @tag external
    test "some test" do
      ...
    end

Or mark description sections

    @tag :external
    describe "some section" do
      test "some test" do
        ...
      end
      ...
    end

Then we can run excluded tests only

    ➜ mix test --only external

Or all project tests

    ➜ mix test --include external

## Debugging

To execute code inside test use

    require IEx; IEx.pry()

## Livebook

To write tests in livebook see [Livebook](../livebook/livebook.md)
