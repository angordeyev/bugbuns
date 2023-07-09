# Erlang

## Debugging

### Inspect

    io:fwrite("--------------------------~n", []),
    'Elixir.IEx.Helpers':i(Object),
    'Elixir.IEx.Helpers':break(),
    io:fwrite("==========================~n", []),

#### Eunit

### Debug Tests and Code

Erlang

    io:format(user, "--------------------\n", []),
    io:format(user, "Text\n", []),
    io:format(user, "====================\n", []),

Elixir

    :io.format(:user, "--------------------\n", [])
    :io.format(:user, "Text\n", [])
    :io.format(:user, "====================\n", [])

### Debug Tests

    ?debugMsg("---------------------"),
    ?debugMsg(?SOME_SOME),
    ?debugMsg("===================="),
