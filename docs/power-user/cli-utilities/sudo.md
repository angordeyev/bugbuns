# sudo

Preserve a user environment when running a command:

```shell
sudo -E <command>
```

Change a user:

```shell
# Change a auser
su <user>

# Change a user to root (you should know root password)
su

# change a user to root (using supervisor password)
sudo su
```

Execute a command as another user:

```shell
sudo -e <user> <command>
```

Change a user and execute a command:

```shell
sudo -u <user> echo 1
sudo su <user> -c 'echo 1; echo 2'
```

`sudo` multiple commands:

```shell
sudo su -c 'echo 1; echo 2'
sudo sh -c 'echo 1; echo 2'
```
