# [rEFInd Boot Manager](https://www.rodsbooks.com/refind/)

## Shortcuts

<kbd>Esc</kbd> - Show rEFInd on startup

## Concepts

ESP - The EFI system partition for the UEFI boot loader

## Installation on a New Device

Show devices

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

[Downlod rEFInd binary zip file](https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download
) from [Getting rEFInd page](https://www.rodsbooks.com/refind/getting.html) or using the dowlnlaod link.

    wget -O /tmp/refind-bin-0.14.0.2.zip https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download

Unzip archive

    unzip /tmp/refind-bin-0.14.0.2.zip

Mount boot partition

    sudo mount -m ${DISK}1 /tmp/boot

Copy the content to the `/tmp/boot` directory

    sudo mkdir -p /tmp/boot/EFI && sudo cp -r /tmp/refind-bin-0.14.0.2/refind $_
