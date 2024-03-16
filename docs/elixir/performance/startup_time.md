# BEAM Startup Time

## Measuring

```shell
time erl -mode minimal -noinput -boot no_dot_erlang -eval "erlang:halt()"
```

```shell
strace -c erl -mode minimal -noinput -boot no_dot_erlang -eval "erlang:halt()"
```

```shell
time erl -mode minimal -noinput -boot start_clean -eval "erlang:halt()"
```

```shell
time erl -mode embedded -noinput -boot no_dot_erlang -eval "erlang:halt()"
```

More information:

```shell
time erl -init_debug -mode minimal -noinput -boot no_dot_erlang -eval "erlang:halt()"
```

Emulator flags:

https://github.com/erlang/otp/blob/master/erts/doc/references/erl_cmd.md#emu_flags

```shell
time erl +ssrct -async_shell_start -mode minimal -noinput -boot no_dot_erlang -eval "erlang:halt()"
```

Before halt:

```shell
date +"%T.%6N"
erl -mode minimal -no-shell -boot no_dot_erlang -eval 'os:cmd("date +'%T.%6N' > result.txt")' -eval "erlang:halt()"
cat result.txt
```

```shell
date +"%T.%6N"
erl -mode minimal -async_shell_start -no-shell -boot no_dot_erlang -eval 'os:cmd("date +'%T.%6N' > result.txt")' -eval "erlang:halt()"
cat result.txt
```

Debug:

```shell
time erl -mode embedded -init_debug -noinput -boot no_dot_erlang -eval "erlang:halt()"
```

```shell
erl -eval 'erlang:now(),erlang:now().'
```

## Custom Boot Files

### `.rel`, `.script`, `.boot` Files

The files are locatated at `_build/<environment>/rel/hello/releases/<version>` for a release:

```shell
<application>.rel
start.boot
start_clean.boot
start_clean.script
start.script
```

.rel - [release resource file](https://www.erlang.org/doc/man/rel)

## Resources

* https://github.com/erlang/otp/tree/master/bootstrap
* [The Erlang Runtime System. Erik Stenman.](https://blog.stenmans.org/theBeamBook/)
* [BEAM VM ELI5](https://beam-wisdoms.clau.se/eli5-vm.html)
* [How does the BEAM boots. Peer Strizinger.](https://codesync.global/media/how-the-beam-boots-and-what-can-be-done-about-it-cbv2020-sept/)
* [beam.smp startup time regression. erlang-questions.](https://erlang.org/pipermail/erlang-questions/2014-April/078473.html)
* [RacketD. Run Racket as a daemon, for significantly better startup times.]https://github.com/jFransham/racketd
* [AtomVM](https://github.com/atomvm/AtomVM)
* [Release is the Word. Learn You Some Erlang for Great Good!](https://learnyousomeerlang.com/release-is-the-word)
* [With Flame out - what can we do to speed up Elixir startup times? Elixir Forum.](https://elixirforum.com/t/with-flame-out-what-can-we-do-to-speed-up-elixir-startup-times/60233)
* [Pelemay](https://github.com/zeam-vm/pelemay)
* [Investigating Erlang by reading its system calls. Julia Evans.](https://jvns.ca/blog/2016/05/13/erlang-seems-really-complicated/)
* [ChezScheme startup time. GitHub Comments.]https://github.com/cisco/ChezScheme/issues/263
* [MOSIX Tutorial](https://mosix.cs.huji.ac.il/pub/tutorial.pdf)
* [patches for erlang to run on Nanos](https://github.com/nanovms/erlang)
