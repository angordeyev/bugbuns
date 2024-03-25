# Create a Universal USB Drive

Create a universal USB Drive compatible with Linux, macOS, Windows:

Show block devices:

```
lsblk
```

```shell
# Set a disk:
DISK=</dev/some>
# Delete MBR and GPT data structures:
sudo sgdisk --zap-all ${DISK}
# Create fresh GPT and protective MBR records:
sudo sgdisk --clear ${DISK}
# Create the largest partition with type 0700 Microsoft basic data
sudo sgdisk --new 1:0:0 --typecode 1:0700 ${DISK}
# Get the first partion on the disk
partition_to_format=$(lsblk -pJ $DISK | jq -r '.blockdevices[0].children[0].name')
# Format to exfat wich is compatible with major operating systems
sudo mkfs.exfat ${partition_to_format}
```

Show parition table records:

```shell
sudo gdisk -l ${DISK}
```

Show file system information:

```shell
sudo lsblk -f ${DISK}
```

Show more information:

```shell
sudo lsblk -f ${DISK}
```

```
blkid
```

Change PARTLABEL:

```shell
sudo sgdisk -c 1:<PARTLABEL> ${DISK}
```

Change LABEL:

```shell
# Unmount first
sudo umount <mount_path>

# Set the label
sudo exfatlabel ${DISK}<parition_number> universal
```

Show updated PARTLABEL and LABEL:

```shell
sudo lsblk --output NAME,FSTYPE,PARTLABEL,LABEL ${DISK}
```

Label will be used by a file manager.
