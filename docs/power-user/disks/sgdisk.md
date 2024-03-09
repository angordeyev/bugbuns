# sgdisk

List storage devices:

Or

```shell
fdisk -l
```

Set a disk:

```shell
DISK=</dev/some>
```

Delete MBR and GPT data structures:

```shell
sudo sgdisk --zap-all ${DISK}
```

Create fresh GPT and protective MBR records:

```shell
sudo sgdisk --clear ${DISK}
```

Check parition table records:

```shell
sudo gdisk -l ${DISK}
```

Print a partition table:

```shell
sudo sgdisk --print ${DISK}
```

List partition types:

```shell
sgdisk -L
```

```output
0700 Microsoft basic data
8300 Linux filesystem
ef00 EFI system partition
```

Create a new partition with a type:

```shell
sudo sgdisk -n1:1MiB:2MiB -t1: ${DISK}
```

Print a partition table:

```shell
sudo sgdisk --print ${DISK}
```

## Resouces

* [GUID Partition Table. Wikipedia.](https://en.wikipedia.org/wiki/GUID_Partition_Table)
