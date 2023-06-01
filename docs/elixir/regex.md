## Regular Expressions

### Cheat Sheet

Character classes

    . - any character

Quantifiers

    ? - zero or one
    * - zero or more
    + - one or more

Wildcard

`.*` can be used like a wildcard

    iex> "hello123" =~ ~r/hello.*/
    iex> "123hello" =~ ~r/.*hello/
    iex> "123hello456" =~ ~r/.*hello.*/

### Examples

~r sigil is used for regular expressions.

    # / is the most common delimiter for regular expressions
    iex> ~r/hello/
    ~r/hello/

    iex> ~r(hello)
    ~r/hello/

Simple expession matches "hello" anywhere in the string

    "new hello world" =~ ~r/hello/ # true
    String.match?("new hello world", ~r/hello/) # true, same as above

Text-based match `=~` operator works this way:

For strings:

    "abcd" =~ "bc" # true, right contains left
    "abcd" =~ ""   # true, right contains left
    "abcd" =~ "e"  # false, right does not contain left
    "ab" =~ "ba"   # false, right does not contain left

For regular expressions:

    "new hello world" =~ ~r/hello/ # cotains hello anywhere in the string

`.` is any caracter

    "hello world" =~ ~r/h.llo/ # true
    "h\x21llo world" =~ ~r/h.llo/ # true, any symbol
    "h llo world" =~ ~r/h.llo/ # true, even space
    "h\nllo world" =~ ~r/h.llo/ # true, new line
    "h.llo world" =~ ~r/h.llo/ # true, and dot itself
    "hllo world" =~ ~r/h.llo/  # but the character should be present

    "h.llo world" =~ ~r/h\.llo/ # true, to find the dot itself esape it
    "hello world" =~ ~r/h\.llo/ # false

[xyz] is character range

    "hello world" =~ ~r/he[l]lo world/ # true
    "hello world" =~ ~r/he[abl]lo world/ # true

    "hello world" =~ ~r/he[:alpha]lo world/ # true
    "hello 5 world" =~ ~r/hello [1-5] world/ # true
    "hello world" =~ ~r/hello world/ # true

    "hello [world]" =~ ~r/hello \[world\]/ # true, to find the square brackets themselves escape them

    "hello world" =~ ~r/he[abc]lo world/ # false
    "hello 5 world" =~ ~r/hello [1-4] world/ # false
    "hello 5 world" =~ ~r/hello [6-9] world/ # false
    "hello world" =~ ~r/he[:allnum]lo world/ # false

`^` exception

    "hello world" =~ ~r/h[^a]llo/ # true
    "hello world" =~ ~r/h[^abc!@#]llo/ # true

    "hello world" =~ ~r/h[^e]llo/ # false, any symbol but not "e"
    "h!llo world" =~ ~r/h[^!@#]llo/ # false, any symbol but not !, @, #

`|` enumerates words

    "hello man" =~ ~r/hello|world/ # true
    "world is fine" =~ ~r/hello|world/ # true
    "world hello" =~ ~r/hello|world/ # true

    "no words" =~ ~r/hello|world/ # false

`()` Groups of symbols

    "start hello end" =~ ~r/start (hello|world) end/ # true
    "start hello end" =~ ~r/start (123|[h][e][l][l][o]) end/ # true
    "start no end" =~ ~r/start (hello|world) end/ # false

`\` Meta symbols

    \d [0-9] digit
    \D [^0-9]- not digit
    \w [[:word:]] - letter or digit symbol or "\_"
    \W \[^[:word:]\] - not letter or digit symbol or "\_"
    \s [\f\n\r\t\v] - space
    \S [^\f\n\r\t\v]- not space
    \[[:alpha]\] - letters only
    \b - matches word bounaries - used to match word

    "hello 1" =~ ~r/hello \d/ # true
    "hello !" =~ ~r/hello \W/ # true
    "hello world" =~ ~r/hello\sworld/ # true
    "hello a" =~ ~r/hello [[:alpha:]]/ # true
    "hello п" =~ ~r/hello [[:alpha:]]/ # true
    "hello world" =~ ~r/\bhello\b/ # true

    "hello 1" =~ ~r/hello \D/ # false
    "hello @" =~ ~r/hello [[:alpha:]]/ # false
    "helloworld" =~ ~r/\bhello\b/ # false

Quantifiers

    ? - zero or one
    * - zero or more
    + - one or more
    {n} - certain number of times
    {m, n} - from m to n
    {m,} - from m
    {0,n} - to n

    # Format

    # <meta symbol><quantifier>

    "hello some world" =~ ~r/hello.*world/ # true, .* is used for any string
    "hello some world" =~ ~r/world.*hello/ # false

    "some@emai.org" =~ ~r/\w+@\w+.\w+/ # true
    "@emai.org" =~ ~r/\w+@\w+.\w+/ # false

Modifiers

    "HELLO WORLD" =~ ~r/hello/  # false
    "HELLO WORLD" =~ ~r/hello/i # true, i - caseless

    "h\nllo world" =~ ~r/h.llo/ # false
    "h\nllo world" =~ ~r/h.llo/s # true, s is dotall modifier which helps to match new line

    "hello 123 world" =~ ~r/hello \d{3} world/ # true
    "hello 123 world" =~ ~r/hello [0-9]{3,} world/ # true
    "hello 123 world" =~ ~r/hello [^a-z]{0,5} world/ # true

Examples
