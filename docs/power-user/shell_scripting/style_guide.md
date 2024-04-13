## Style Guide

[Google style guide](https://google.github.io/styleguide/shellguide.html)

### Naming

Function and variable names have snake_case:

```shell
some_function() {
  some_variable=1
}
```

Constant and environment variables have SCREAMING_SNAKE_CASE:

```shell
export SOME_ENV=1
```

### Multiline

space and `\` befor a new line, start next line with double spaces

```shell
curl -X POST httpbin.org/post \
  -H 'Content-Type: application/json' \
  -d '{"login":"my_login","password":"my_password"}'
```

## Environment variables

String interpolation:

```shell
VAR="Hello"

# using ${VAR} in interpolation prevents error
# that $VAR_SOMETHING variable is used insted of ${VAR}
echo "Hello ${VAR}VAR"
```

## Command substitution

Assigninng:

```shell
VAR=$(echo "hello")
echo ${VAR}
```

```output
hello
```

String interpolation:

```shell
echo "hello $(echo "world")"
```

```output
hello world
```

## Arithmetics

Arithmentic extension `$((<expression>))`:

```shell
echo "Helo $((1+1))"
```

Let:

```shell
let VAR=1+1
echo $VAR
```

## Commands

### Quotes

Double quotes are preffered

```cmd
var=world
echo "hello ${var}"
```
```output
hello world
```

Use single quotes to skip interpolation

```cmd
var=world
echo 'hello ${var}'
```
```output
hello ${var}
```

You can user single quotes and double quotes:

```shell
➜ echo 'hello "quotes"'
hello "quotes"

➜ echo "hello 'quotes'"
hello 'quotes'

➜ var=world
➜ echo "hello ${var}" # string inerpolation works
hello world

➜ var=world
➜ echo 'hello ${var}' # string interploation does not work
hello ${var}
```

### Multiline strings

Heredocs is used, EOF - end of text, could be EOT or any other text

Tee works with sudo and allows to supress output (`> /dev/null`)

With interpolation, w

```bash
sudo tee file.txt > /dev/null <<EOF
line 1
line 2
EOF
```
Without interpolation, see quotes for EOF

```bash
sudo tee file.txt > /dev/null <<`EOF`
line 1
line 2
EOF
```

Using `cat`

```bash
cat <<EOF
line 1
line 2
EOF
```

Indented


```bash
  cat << EOF
      line 1
      line 2
EOF
```

To allign last `EOF` use first EOF with preceeding spaces

```bash
    cat << '    EOF'
      line 1
      line 2
    EOF
```

Save to file

```bash
cat <<EOF > file.txt
line 1
line 2
EOF
```

With indentation:

```shell
readarray message <<'   EOF'
    Hello, this is a cool program.
    This should get unindented.
    This code should stay indented:
            something() {
                    echo It works, yo!;
            }
    That is all.
EOF
```

## `[ exression ]` vs `[[ expresion ]]`

Use `[[ expresion ]]`

## Resources

* [Google style guide](https://google.github.io/styleguide/shellguide.html)
* [What's the difference between \[ and \[\[. StackOverflow](https://stackoverflow.com/questions/3427872/whats-the-difference-between-and-in-bash)
