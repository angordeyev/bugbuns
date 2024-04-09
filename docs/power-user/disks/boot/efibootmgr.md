# efibootmgr

## Tasks

### Show Entries

```shell
efibootmgr
```

### Create an entry

Show EFI partitions:

```shell
lsblk \
  --output ID,NAME,SIZE,PARTUUID,PARTLABEL,FSTYPE \
  --filter 'PARTTYPENAME == "EFI System"'
```

Create an entry (the entry will be crated for the first partition by default):

```shell
efibootmgr -c -d /dev/sdc -L "Experimental rEFInd" -l '\EFI\refind\refind_x64.efi'
```

### Delete an Entry

```shell
sudo efibootmgr --delete-bootnum --bootnum 0000
```

## Resources

* [UEFI boot: how does that actually work, then? AdamW on Linux and more.](https://www.happyassassin.net/posts/2014/01/25/uefi-boot-how-does-that-actually-work-then/)
