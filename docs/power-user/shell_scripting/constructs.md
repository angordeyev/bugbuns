# Constructs

## Multiline Single Command

```cmd
ls \
  -la
```

## Singleline Multiple Commands

```cmd
ls; ls
```

## Command Substitution

```cmd
ls $(echo "-la")
```

## Arithmetic Expression

Evaluates an expression but does not store the result

```bash
((1 + 1)) ; echo $?
```

```output
0
```

```bash
((0 < 1)); echo $?
```

```output
0
```

```bash
((0 > 1)); echo $?
```

```output
1
```

`$((expression))` stores a result

```bash
echo $((1 + 1))
```

```output
2
```

## If

```bash
a=1
if [[ ${a} == 1 ]]; then
  echo "hello"
fi
```

```output
hello
```

```bash
a=1
if [ ${a} = 0 ]; then
  echo "hello"
else
  echo "world"
fi
```

```output
world
```

Singleline

```bash
if [[ 0 < 1 ]]; then; echo "hello"; fi
```

```output
hello
```

```bash
if [[ 0 > 1 ]]; then; echo "hello"; fi
```

```output
```

## while

```bash
a=1
while [[ ${a} < 3 ]]; do
  echo ${a}
  a=$((a + 1))
done
```

```output
1
2
```

## for

```bash
for a in 1 2 3
do
  echo ${a}
done
```

```output
1
2
3
```

