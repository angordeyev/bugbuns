# Tasks

## Show Storage Devices

```shell
sudo fdisk -l
```

```shell
sudo lsblk -o NAME,SIZE,ID,ID-LINK,PTUUID \
  --filter 'TYPE == "disk"'
```

ID-LINK - same as `/dev/disk/by-id`
PTUUID - partition Table ID (it will be empty if parition table is missing)

## Show Partitions

```shell
sudo lsblk \
  --output NAME,SIZE,ID,PTUUID,UUID,PARTTYPENAME,PARTLABEL,LABEL \
  --filter 'TYPE == "part"'
```

## Inform the Kernel About Partition Changes

```shell
sudo partprobe
```

## Create a Full Disk ext4 Partition

```shell
DISK=<DISK>
PARTLABEL=<PARTLABEL>

# Delete MBR and GPT data structures
sudo sgdisk --zap-all ${DISK}

# Create fresh GPT and protective MBR records
sudo sgdisk --clear ${DISK}

# Create the largest partition with type 0700 Microsoft basic data:
# --new=partnum:start:end             create new partition
# --typecode=partnum:{hexcode|GUID}   change partition type code
# 8300 - Linux partition (`sgdisk -L` to list types)
sudo sgdisk --new 1:0:0 --typecode 1:8300 ${DISK}

# Change the partition label
sudo sgdisk -c 1:${PARTLABEL} ${DISK}

# Change the volume label
sudo mkfs.ext4 -L ${PARTLABEL} ${DISK}1
```

## A Permanent Mount

Add to `/etc/fstab`:

```shell
LABEL=<LABEL>    /mnt/ex    ext4    rw,relatime    0    2
```

## Resources

* [fstab. archlinux wiki.](https://wiki.archlinux.org/title/Fstab)
