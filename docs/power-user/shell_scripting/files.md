# Working with Files

## Crate a File and Parent Directories

```shell
file="/tmp/some/file.txt"
# Create the parent directories if they do not exist
mkdir -p $(dirname ${file})
touch ${file}
```

## Write to a New File

Using `cat`:

```shell
file="/tmp/some/file.txt"
# Create the parent directories if they do not exist
mkdir -p $(dirname ${file})

cat <<EOF > ${file}
Some
Text
EOF
```

```shell
cat > ${file} <<EOF
Some
Text
EOF
```

Using `tee`:

```shell
file="/tmp/some/file.txt"
# Create the parent directories if they do not exist
mkdir -p $(dirname ${file})

tee /tmp/some_file.txt <<EOF
Some
Text
EOF
```

Using `tee` and hiding output:

```shell
file="/tmp/some/file.txt"
# Create the parent directories if they do not exist
mkdir -p $(dirname ${file})

tee /tmp/some_file.txt > /dev/null <<EOF
Some
Text
EOF
```

## Appent to a File

```shell
cat << EOF >> /tmp/some/file.txt

Appended
Text
EOF
```

```shell
cat <<EOF
Appended
Text
EOF
```


