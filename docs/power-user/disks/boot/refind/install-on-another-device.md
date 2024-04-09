# Install on Another Device

Show the system devices:

```shell
lsblk
```

Install:

```shell
# Mount partition
sudo mount ${DISK_PARTITION} /mnt/boot

# Download
wget -O /tmp/refind-bin.zip https://sourceforge.net/projects/refind/files/0.14.1/refind-bin-0.14.1.zip/download

# Unzip archive
cd /tmp && unzip /tmp/refind-bin.zip && cd refind-bin-0.14.1

# Install rEFInd to the default folder
sudo ./refind-install --root /mnt

# Unmount
sudo umount /mnt/boot
```

Check if a EFI entry is created:

```shell
efibootmgr
```

```output
Boot0000* rEFInd Boot Manager HD(1,GPT,9b2bdfea-a3ed-486f-a74b-ddbee8176963,0x800,0x200000)/\EFI\refind\refind_x64.efi
```
