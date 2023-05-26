# Keys

# Working with Keys

Read arrow keys

```bash
esc=$(echo -en "\e") # cache ESC as test doesn't allow esc codes
read -s -n3 key

if [[ $key == $esc[A ]]; then
    echo "up"
elif [[ $key == $esc[B ]]; then
    echo "down"
else
    echo "other"
fi
```

Move in a terminal

```bash
echo "1"
echo "2"
echo "3"

esc=$(echo -en "\e") # cache ESC as test doesn't allow esc codes

while true 
do
  read -s -n3 key # wait for user to key in arrows or ENTER
  if [[ $key == $esc[A ]] # up arrow
  then
      echo -en "\e[1A"
  elif [[ $key == $esc[B ]] # down arrow
  then
      echo -en "\e[1B"
  fi
done
```

## Resources

[How can I create a select menu in a shell script? By Gusss on AskUbuntu](https://askubuntu.com/a/1386907/1672230)
