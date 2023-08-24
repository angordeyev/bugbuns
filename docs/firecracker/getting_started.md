# Getting Started

## Get a Kernel

Download a kernel tarbal at [Linux Kernel Archive](https://www.kernel.org/).

Unpack the archive and go into the folder.

Run and save the config:

```sh
make menuconfig
```

Run for `x86_64` platform:

```shell
make vmlinux
```

There is `vmlinux` after compilation.

## Create rootfs Image

Prepare a properly-sized file.

```shell
dd if=/dev/zero of=rootfs.ext4 bs=1M count=50
````

Create an empty file system:

```shell
mkfs.ext4 rootfs.ext4
```
