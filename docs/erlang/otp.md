# Erlang OTP

## Fast BEAM Start

https://codesync.global/media/how-the-beam-boots-and-what-can-be-done-about-it-cbv2020-sept/

## erlc

```erl
-module(hello).
-export([start/0]).

start() ->
    io:fwrite("Hello, world!\n").
```

```sh
erlc hello.erl
```

```sh
timeout 0.003s sleep 0.001 && echo foo
```

```sh
timeout 0.003s erl -noshell -eval 'io:fwrite("Hello, World!\n"), init:stop().'
```


```sh
timeout 0.003s erl -noshell -s hello start -s init stop
```

## Resources

* [Erlang-BEAM-Links](https://github.com/AlexanderKaraberov/Erlang-BEAM-Links)
* [How the BEAM boots and what can be done about it](https://codesync.global/media/how-the-beam-boots-and-what-can-be-done-about-it-cbv2020-sept/)
* https://elixirforum.com/t/how-to-minimise-beam-startup-time/31913
* https://github.com/erlang/otp/blob/master/erts/etc/common/erlc.c#L287
* https://www.erlang.org/doc/system_principles/system_principles.html


