# AtomVM

## Getting Started

Clone the repository:

```shell
git clone git@github.com:atomvm/AtomVM.git
```

Build:

```shell
mkdir build
cd build
cmake ..
make
```

Edit the Elixir application at `AtomVM/examples/elixir/HelloWorld.ex`.

Compile the Elixir application:

```shell
make HelloWorld
```

Run the application:

```shell
./src/AtomVM ./examples/elixir/HelloWorld.avm
```
