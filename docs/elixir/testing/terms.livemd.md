# Terms

```elixir
Mix.install([
  {:mimic, "~> 1.7"}
])
```

## Code

```elixir
defmodule Calculator do
  def add(x, y) do
    x + y
  end
end
```

## List of Terms

* Dummy - simple object to pass as an argument

* Fake  - object contains predefined data and no logic

* Stub  - ojbect used instead of a real object

* Mock  - a stub object with defined expectations (used as a general term)

* Expectation - a checked condition mock object function is called

* Fixture - group ob objects, test context, test state

* Test Factory -

## Fake

Contains data and no logic.

```elixir
Mimic.copy(Calculator)
ExUnit.start()

defmodule CalculatorFake do
  def add(x, y) do
    data = %{
      {1, 0} => 1,
      {0, 1} => 1,
      {1, 1} => 2,
      {1, 2} => 3
    }

    data[{x, y}]
  end
end

defmodule CalcutorFakeTest do
  use ExUnit.Case
  use Mimic

  test "fake module" do
    Calculator
    |> stub_with(CalculatorFake)

    assert Calculator.add(1, 0) == 1
  end

  test "stub function" do
    Calculator
    |> stub(:add, fn x, y ->
      data = %{
        {1, 0} => 1,
        {0, 1} => 1,
        {1, 1} => 2,
        {1, 2} => 3
      }

      data[{x, y}]
    end)

    assert Calculator.add(1, 1) == 2
  end
end
```

## Stub

Stub is an object that replaces a real object

```elixir
Mimic.copy(Calculator)
ExUnit.start()

defmodule CalculatorStub do
  def add(_x, _y) do
    1
  end
end

defmodule CalcutorStubTest do
  use ExUnit.Case
  use Mimic

  test "stub module" do
    Calculator
    |> stub_with(CalculatorStub)

    assert Calculator.add(1, 0) == 1
  end

  test "stub function" do
    Calculator
    |> stub(:add, fn _x, _y -> 2 end)

    assert Calculator.add(1, 1) == 2
  end
end

ExUnit.run()
```

## Mock

Mock is an object that register calls and verify calls it receives

```elixir
Mimic.copy(Calculator)
ExUnit.start()

defmodule CalcutorMockTest do
  use ExUnit.Case
  use Mimic

  test "mock" do
    # mock Calculator
    Calculator
    |> expect(:add, fn _x, _y -> 3 end)

    assert Calculator.add(1, 2) == 3
  end
end

ExUnit.run()
```

## Resources

[What's the difference between a mock & stub?](https://stackoverflow.com/questions/346372/whats-the-difference-between-faking-mocking-and-stubbing)
