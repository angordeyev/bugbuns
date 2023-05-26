# Erase Data

    ERASE_DISK=/dev/sd<i>
    sudo dd if=/dev/zero of=${ERASE_DISK} bs=1M status=progress
