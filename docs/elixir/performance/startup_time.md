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

* [RacketD. Run Racket as a daemon, for significantly better startup times.]https://github.com/jFransham/racketd
* [AtomVM](https://github.com/atomvm/AtomVM)
* [Release is the Word. Learn You Some Erlang for Great Good!](https://learnyousomeerlang.com/release-is-the-word)
* [With Flame out - what can we do to speed up Elixir startup times? Elixir Forum.](https://elixirforum.com/t/with-flame-out-what-can-we-do-to-speed-up-elixir-startup-times/60233)
* [Pelemay](https://github.com/zeam-vm/pelemay)
* [Investigating Erlang by reading its system calls. Julia Evans.](https://jvns.ca/blog/2016/05/13/erlang-seems-really-complicated/)
* [ChezScheme startup time. GitHub Comments.]https://github.com/cisco/ChezScheme/issues/263
* [MOSIX Tutorial](https://mosix.cs.huji.ac.il/pub/tutorial.pdf)
