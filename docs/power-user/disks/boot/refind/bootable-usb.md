# Quick USB Install

Show the system devices:

```shell
lsblk
```

Set a ESP to install rEFInd:

```shell
DISK=/dev/<device>
```

Prepare the disk for a new system Installation, **be careful it will delete the disk data!**:

```shell
# Reload the partition
sudo partprobe $DISK

# Delete partition tables from the device and create the fresh partition tables
sudo wipefs --all --force $DISK   # Delete signatures/metadata/magic
sudo sgdisk --zap-all $DISK       # Delete GPT and MBR
sudo sgdisk --clear $DISK         # Create fresh GPT and protective MBR

# Create the partitions
sudo sgdisk -n1:2048:+1G -t1:EF00 $DISK   # ESP
sudo sgdisk -n2 $DISK                       # Remaining space for Linux partition

# Get the partitions names
DISK1=/dev/$(sudo lsblk -J ${DISK} | jq -r '.blockdevices[0].children[0].name')
DISK2=/dev/$(sudo lsblk -J ${DISK} | jq -r '.blockdevices[0].children[1].name')

# Format the partitions
sudo mkfs.vfat ${DISK1} # ESP
sudo mkfs.ext4 ${DISK2} # Linux parition
```

Run the script below, **be careful it will overwrite the disk data!**:

```shell
# Install rEFInd to the default folder
sudo refind-install --usedefault ${DISK1}

# Mount partition
sudo mount ${DISK1} /mnt/boot

# Change timeout to load the default OS immediately
sudo sed -i 's/timeout.*/timeout -1/' /mnt/boot/EFI/BOOT/refind.conf

# Change resolution
sudo sed -i 's/#resolution 1024 768.*/resolution 1920 1080/' /mnt/boot/EFI/BOOT/refind.conf

# Unmount
sudo umount /mnt/boot
```
