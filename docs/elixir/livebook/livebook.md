# Livebook

## Installation

Install Livebook

    mix escript.install hex livebook

Run if using asdf

    asdf reshim

## Commands

### Using Command Line Arguments

Run livebooks

    ➜ livebook server # run livebook
    ➜ livebook server <file.livemd> # open file
    ➜ livebook server ./ # open the current directory
    ➜ livebook server /home/user/livebooks # open an absolute path directory

Run livebooks on a node/mix project

    ➜ livebook server --default-runtime attached:<node@host>:<cookie> <file_or_folder>
    ➜ livebook server --default-runtime mix:/path/to/project <file.livemd>

### Using Environment Variables

    ➜ LIVEBOOK_DEFAULT_RUNTIME=mix:/path/to/project livebook server file.livemd
    ➜ LIVEBOOK_DEFAULT_RUNTIME=attached:<node@host>:<cookie> livebook server file.livemd

## Adding dependencies

**Warning**

If you write code in "Dependencies and startup" in will dissapear when you left the block.

Set in reconnect and setup section:

    Mix.install([:ecto])

## Writing Tests

Setup tests in each test or in setup block

    ExUnit.start()

Then run test

    defmodule SomeTest do
      use ExUnit.Case

      test "check if assert works" do
        assert 1 == 1
      end
    end
    ExUnit.run() # Important, run ExUnit.run() at the end of a code block

## Shell

    {output, 0} = System.shell("
      touch 1.txt
      echo 'line 1' >> 1.txt
      echo 'line 2' >> 1.txt
      cat 1.txt
    ")
    IO.puts(output) # IO puts formats output using, otherwise it rerurns one line with '\n' character

Creating mix project

    System.shell("mix new hello_tmp &")
    System.shell("ls -la")

TODO if the programs asks for a user input it will stuck

## Troubleshooting

### No preset version installed for command livebook

    asdf reshim

[No preset version installed for command livebook. Elixir Forum.](https://elixirforum.com/t/no-preset-version-installed-for-command-livebook/45807)

## Resources

[Livebook for Elixir: Just What the Docs Ordered](https://blog.appsignal.com/2022/05/24/livebook-for-elixir-just-what-the-docs-ordered.html)
[Connecting Livebook to Your App in Production](https://fly.io/docs/app-guides/elixir-livebook-connection-to-your-app/)


