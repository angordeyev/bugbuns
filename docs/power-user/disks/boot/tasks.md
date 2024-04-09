# Tasks

Task-centered approach.

## Shortcuts

<kbd>F2></kbd> - Enter UEFI on many systems
<kbd>Esc</kbd> - Show rEFInd on startup

## Managing EFI[^1] Boot Entries

Show boot entries:

```shell
sudo efibootmgr
```

Change an order:

```shell
sudo efibootmgr --bootorder 0,1,2,3,b
```

Remove boot entries from the list using `Boot000<i>` index

```shell
sudo efibootmgr -b <i> -B # remove the item with name Boot000i
```

Show PARTUUIDs used in ESPs:

```shell
sudo blkid -s PARTUUID -t TYPE=vfat
```

```shell
sudo lsblk -o NAME,SIZE,PARTUUID,PARTLABEL,FSTYPE \
  --filter 'PARTTYPENAME == "EFI System"'
```

## Resources

* [Where is the UEFI boot order stored?. StackOverflow.](https://superuser.com/questions/955525/where-is-the-uefi-boot-order-stored)
* [UEFI boot: how does that actually work, then? AdamW on Linux and more.](https://www.happyassassin.net/posts/2014/01/25/uefi-boot-how-does-that-actually-work-then/)

## Footnotes

[^1]: Extensible Firmware Interface
