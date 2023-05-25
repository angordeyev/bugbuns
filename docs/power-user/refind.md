# rEFInd

Working with rEFInd boot manager

## Concepts

ESP - EFI system partition for a UEFI boot manager

## Quick Install

Set a ESP to install rEFInd

    DISK=/dev/sd<x><y>

Run the script below. **Be careful it will overwrite the disk data!**

    # Install refind to the default folder
    sudo refind-install --usedefault ${DISK}

    # Mount partition
    sudo mount ${DISK} /mnt/boot

    # Change timeout to load the default OS immediately
    sudo sed -i 's/timeout.*/timeout -1/' /mnt/boot/EFI/refind/refind.conf

    # Change resolution
    sudo sed -i 's/#resolution 1024 768.*/resolution 1920 1080/' /mnt/boot/EFI/refind/refind.conf

## Shortcuts

<kbd>F2></kbd> - Enter UEFO on many systems
<kbd>Esc</kbd> - Show rEFInd on startup

## Site

https://www.rodsbooks.com/refind/

## Prepare the Disk for a New System Installation

Show the system devices

    lsblk

Set disk value

    DISK=/dev/<disk>

Delete partition tables from the device and create the fresh partition tables

    sudo wipefs --all --force $DISK   # Delete signatures/metadata/magic
    sudo sgdisk --zap-all $DISK       # Delete GPT and MBR
    sudo sgdisk --clear $DISK         # Create fresh GPT and protective MBR

Warining: The kernel is using the old partition table. Reboot.

    sudo sgdisk -n1:2048:+512M -t1:EF00 $DISK   # ESP
    sudo sgdisk -n2 $DISK                       # Remaining space for Linux partition

Format the partition

    sudo mkfs.vfat ${DISK}1 # ESP
    sudo mkfs.ext4 ${DISK}2 # Linux parition

Reload the partitions in the OS

    sudo partprobe $DISK

## Manual Installation

Check the latest version by going to [rEFInd page](https://www.rodsbooks.com/refind/getting.html)

[Download](https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download) rEFInd binary zip file

    wget -O /tmp/refind-bin-0.14.0.2.zip https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download

Unzip archive

    unzip /tmp/refind-bin-0.14.0.2.zip

Mount boot partition

    sudo mount -m ${DISK}1 /mnt/boot # or sudo mount -o X-mount.mkdir ${DISK}1 /mnt/boot

Copy the content to the `/mnt/boot` directory

    sudo mkdir -p /mnt/boot/EFI && sudo cp -r /tmp/refind-bin-0.14.0.2/refind $_

Rename the directoy and the file to the default UIFI names if required (useful for removable flash USB drives)

    sudo mv /mnt/boot/EFI/refind /mnt/boot/EFI/BOOT

    sudo mkdir -p /mnt/boot/EFI && sudo cp -r /tmp/refind-bin-0.14.0.2/refind $_

Rename the rEFInd config

    sudo mv /mnt/boot/EFI/refind/refind.conf-sample /mnt/boot/EFI/refind/refind.conf

Check if rEFIind boot manager exist

    sudo efibootmgr -v

Add rEFInd to EFI's list of available bootloaders **if the default path is not used**

    sudo efibootmgr -d ${DISK} -c -l  \\EFI\\refind\\refind_x64.efi -L rEFInd

## Manage EFI Boot Entries

Show boot entries

    sudo efibootmgr

Remove boot entries in the list, using `Boot000<i>` index

    sudo efibootmgr -b <i> -B # remove the item with name Boot000i

Show PARTUUIDs used in ESPs

    sudo blkid -s PARTUUID -t TYPE=vfat

## Configure rEFInd

Mount the EFI partition

    DISK=/dev/<disk>
    
    sudo mount -m ${DISK}1 /mnt/boot # or sudo mount -o X-mount.mkdir ${DISK}1 /mnt/boot

Change timeout to load the default OS immediately

    sudo sed -i 's/timeout.*/timeout -1/' /tmp/boot/EFI/refind/refind.conf

Change resolution

    sudo sed -i 's/#resolution 1024 768.*/resolution 1920 1080/' /mnt/boot/EFI/refind/refind.conf

## Theming

[Refind theming page](https://www.rodsbooks.com/refind/themes.html)
[GitHub rEFInd topic](https://github.com/topics/refind)
[rEFIind page in Arch Linux wiki](https://wiki.archlinux.org/title/REFInd)
