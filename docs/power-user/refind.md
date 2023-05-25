# rEFInd

Working with rEFInd boot manager

## Shortcuts

<kbd>F2></kbd> - Enter UEFO on many systems
<kbd>Esc</kbd> - Show rEFInd on startup

## Concepts

ESP - The EFI system partition for the UEFI boot manager

## Site

https://www.rodsbooks.com/refind/

## Installation on a New Device

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

Check the lates version by going to [rEFInd page](https://www.rodsbooks.com/refind/getting.html)

[Download](https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download) rEFInd binary zip file

    wget -O /tmp/refind-bin-0.14.0.2.zip https://sourceforge.net/projects/refind/files/0.14.0.2/refind-bin-0.14.0.2.zip/download

Unzip archive

    unzip /tmp/refind-bin-0.14.0.2.zip

Mount boot partition

    sudo mount -m ${DISK}1 /tmp/boot

Copy the content to the `/tmp/boot` directory

    sudo mkdir -p /tmp/boot/EFI && sudo cp -r /tmp/refind-bin-0.14.0.2/refind $_

Rename the rEFInd config

    sudo mv /tmp/boot/EFI/refind/refind.conf-sample /tmp/boot/EFI/refind/refind.conf

Check if rEFIind boot manager exist

    sudo efibootmgr -v

Add rEFInd to EFI's list of available bootloaders

    sudo efibootmgr -d ${DISK} -c -l  \\EFI\\refind\\refind_x64.efi -L rEFInd

## Manage EFI Boot Entries

Show boot entries

    sudo efibootmgr

Remove boot entries in the list, using `Boot000<i>` index

    sudo efibootmgr -b <i> -B # remove the item with name Boot000i

Show PARTUUIDs used in boot entries

    sudo blkid -s PARTUUID

## Configure rEFInd

Mount the EFI partition

    DISK=/dev/<disk>
    sudo mount -m ${DISK}1 /tmp/boot

Change timeout to load the default OS immediately

    sudo sed -i 's/timeout.*/timeout -1/' /tmp/boot/EFI/refind/refind.conf

Change resolution

    sudo sed -i 's/#resolution 1024 768.*/resolution 1920 1080/' /tmp/boot/EFI/refind/refind.conf

## Theming

[Refind theming page](https://www.rodsbooks.com/refind/themes.html)
[GitHub rEFInd topic](https://github.com/topics/refind)
