# rEFInd

Working with rEFInd boot manager.

## Getting Help

[REFIND-INSTALL Man Page](https://www.rodsbooks.com/refind/refind-install.html)

```shell
man refind-install
```

## Concepts

ESP - EFI system partition for a UEFI boot manager.

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

Set DISK variable:

```shell
DISK=/dev/<disk>
```

Create new partitions:

```shell
sudo partprobe $DISK              # Reload the partitions in the OS
sudo wipefs --all --force $DISK   # Delete signatures/metadata/magic
sudo sgdisk --zap-all $DISK       # Delete GPT and MBR
sudo sgdisk --clear $DISK         # Create fresh GPT and protective MBR
sudo partprobe $DISK              # Reload the partitions in the OS
```

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
wget -O /tmp/refind-bin.zip https://sourceforge.net/projects/refind/files/0.14.1/refind-bin-0.14.1.zip/download
```

Unzip archive:

```shell
unzip /tmp/refind-bin.zip
```

Mount boot partition:

```shell
sudo mount -m ${DISK}1 /mnt/boot # or sudo mount -o X-mount.mkdir ${DISK}1 /mnt/boot
```

Copy the content to the `/mnt/boot` directory

```shell
sudo mkdir -p /mnt/boot/EFI && sudo cp -r /tmp/refind-bin-0.14.1/refind $_
```

Rename the directory and the file to the default UIFI names if required (useful for removable flash USB drives)

```shell
sudo mv /mnt/boot/EFI/refind /mnt/boot/EFI/BOOT
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
