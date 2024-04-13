# tee

```shell
# tee writes to stdout and to file
echo hello | tee hello.txt

# using sudo and hiding ouput
echo hello2 | sudo tee hello.txt > /dev/null
```
