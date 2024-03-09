# rEFInd

Working with rEFInd boot manager.

## Concepts

ESP - EFI system partition for a UEFI boot manager.

## Quick Install

Show the system devices:

```shell
lsblk
```

Set a ESP to install rEFInd

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

## Shortcuts

<kbd>F2></kbd> - Enter UEFI on many systems
<kbd>Esc</kbd> - Show rEFInd on startup

## Site

https://www.rodsbooks.com/refind/

## Prepare the Disk for a New System Installation

Show the system devices

```shell
lsblk
```

Set disk value

```shell
DISK=/dev/<disk>
```

Delete partition tables from the device and create the fresh partition tables:

```shell
sudo wipefs --all --force $DISK   # Delete signatures/metadata/magic
sudo sgdisk --zap-all $DISK       # Delete GPT and MBR
sudo sgdisk --clear $DISK         # Create fresh GPT and protective MBR
```

Warining: The kernel is using the old partition table. Reboot.

```shell
sudo sgdisk -n1:2048:+512M -t1:EF00 $DISK   # ESP
sudo sgdisk -n2 $DISK                       # Remaining space for Linux partition
```

Format the partition:

```shell
sudo mkfs.vfat ${DISK}1 # ESP
sudo mkfs.ext4 ${DISK}2 # Linux parition
```

Reload the partitions in the OS:

```shell
sudo partprobe $DISK
```

## Manual Installation

Check the latest version by going to [rEFInd page](https://www.rodsbooks.com/refind/getting.html)

[Download](https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download) rEFInd binary zip file

```shell
wget -O /tmp/refind-bin-0.14.0.2.zip https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download
```

Unzip archive

```shell
unzip /tmp/refind-bin-0.14.0.2.zip
```

Mount boot partition

```shell
sudo mount -m ${DISK}1 /mnt/boot # or sudo mount -o X-mount.mkdir ${DISK}1 /mnt/boot
```

Copy the content to the `/mnt/boot` directory

```shell
sudo mkdir -p /mnt/boot/EFI && sudo cp -r /tmp/refind-bin-0.14.0.2/refind $_
```

Rename the directoy and the file to the default UIFI names if required (useful for removable flash USB drives)

```shell
sudo mv /mnt/boot/EFI/refind /mnt/boot/EFI/BOOT

sudo mkdir -p /mnt/boot/EFI && sudo cp -r /tmp/refind-bin-0.14.0.2/refind $_
```

Rename the rEFInd config

```shell
sudo mv /mnt/boot/EFI/refind/refind.conf-sample /mnt/boot/EFI/refind/refind.conf
```

Check if rEFIind boot manager exist

```shell
sudo efibootmgr -v
```

Add rEFInd to EFI's list of available bootloaders **if the default path is not used**

```shell
sudo efibootmgr -d ${DISK} -c -l  \\EFI\\refind\\refind_x64.efi -L rEFInd
```

## Manage EFI Boot Entries

Show boot entries

```shell
sudo efibootmgr
```

Remove boot entries in the list, using `Boot000<i>` index

```shell
sudo efibootmgr -b <i> -B # remove the item with name Boot000i
```

Show PARTUUIDs used in ESPs

```shell
sudo blkid -s PARTUUID -t TYPE=vfat
```

## Configure rEFInd

Mount the EFI partition

```shell
    DISK=/dev/<disk>

    sudo mount -m ${DISK}1 /mnt/boot # or sudo mount -o X-mount.mkdir ${DISK}1 /mnt/boot
```

Change timeout to load the default OS immediately

```shell
sudo sed -i 's/timeout.*/timeout -1/' /tmp/boot/EFI/refind/refind.conf
```

Change resolution

```shell
sudo sed -i 's/#resolution 1024 768.*/resolution 1920 1080/' /mnt/boot/EFI/refind/refind.conf
```

## Theming

* [Refind theming page](https://www.rodsbooks.com/refind/themes.html)
* [GitHub rEFInd topic](https://github.com/topics/refind)
* [rEFIind page in Arch Linux wiki](https://wiki.archlinux.org/title/REFInd)
