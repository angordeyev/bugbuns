---
draft: true
---

# Watchdog

Настройка Watchdog в виртуальной машине oVirt 4.0 с гостевой ОС Debian 8.6
Для начала в oVirt настраиваем в свойствах виртуальной машины поддержку Watchdog Device, как это было писано ранее. Затем переходим в гостевую ОС Debian 8.6 и проверяем появилось ли в системе устройство:

# lspci | grep watchdog -i

00:08.0 System peripheral: Intel Corporation 6300ESB Watchdog Timer
Установим службу:

# apt install watchdog
Сделаем минимальную корректировку конфигурационного файла /etc/watchdog.conf, то есть уберём комментарий в одной строке (другие параметры настраиваются при необходимости в зависимости от ваших потребностей):

/etc/watchdog.conf
...
#
watchdog-device = /dev/watchdog
#
...
Проверим наличие модуля ядра с драйвером для поддержки нашего устройства. Команда загрузки модуля не должна выдавать ошибок:

# modprobe i6300esb
Затем отредактируем файл /etc/default/watchdog, в частности в строку watchdog_module=«none» впишем имя нашего модуля и при необходимости добавляем параметры watchdog_options. В итоге файл должен принять следующий вид:

/etc/default/watchdog
# Start watchdog at boot time? 0 or 1
run_watchdog=1
# Start wd_keepalive after stopping watchdog? 0 or 1
run_wd_keepalive=1
# Load module before starting watchdog
watchdog_module="i6300esb"
# Specify additional watchdog options here (see manpage).
watchdog_options="-s -c /etc/watchdog.conf"


`virt-install` has `--watchdog` parameter.

Show available OSes:

```shell
virt-install --osinfo list
```

```shell
osinfo-query os
```

See networks:

```shell
sudo virsh net-list --all
```

Activate a network:

```shell
sudo virsh net-start default
```

Install from network:

```shell
export VM_NAME="debian"
export VM_ISO="https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.5.0-amd64-netinst.iso"
export VM_URL="http://ftp.us.debian.org/debian/dists/stable/main/installer-amd64/"
export VM_OS="debian12"
# export VM_IMG="/data/libvirt/images/${VM_NAME}.qcow2"
export VM_CORES=1
export VM_DISKSIZE=10
export VM_RAMSIZE=2048
export VM_NET="default"

sudo virt-install \
  --name ${VM_NAME} \
  --memory ${VM_RAMSIZE} \
  --vcpus ${VM_CORES} \
  --os-variant=${VM_OS} \
  --virt-type=kvm \
  --network network=${VM_NET},model=virtio \
  --graphics none \
  --disk path=${VM_IMG},size=${VM_DISKSIZE},bus=virtio,format=qcow2 \
  --location ${VM_URL} \
  --extra-args="console=ttyS0"
```

```shell
 virt-install \
  --name debian \
  --memory 2048 \
  --vcpus 2 \
  --disk size=8 \
  --location https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.5.0-amd64-netinst.iso \
  --os-variant debianbookworm
```

An example:

```shell
virt-install --virt-type kvm --name MyCentosVM --ram 2048 \
  --disk /var/lib/libvirt/images/mycentosvm.qcow2,size=40,format=qcow2 \
  --network network=default \
  --os-type=linux --os-variant=centos7.0 \
  --location=/install/CentOS-7-x86_64-Minimal-2009.iso \
  --graphics none \
  --console pty,target_type=serial \
  --extra-args 'console=ttyS0,115200n8 serial
```

```shell
virt-install \
  --memory 2048 \
  --vcpus 2 \
  --name tst \
  --disk /var/lib/libvirt/images/tst/tst.qcow2,device=disk \
  --disk /var/lib/libvirt/images/tst/config.iso,device=cdrom \
  --os-type Linux \
  --os-variant centos7.0 \
  --virt-type kvm \
  --graphics none \
  --network default \
  --import
```


Query OSes:

## Freeze Linux System

```shell
echo c > /proc/sysrq-trigger
```

## Resources

* https://wiki.it-kb.ru/ovirt/ovirt-kvm-how-to-install-watchdog-service-in-guest-os-debian-8-6
* [virt-install. man.](https://man.archlinux.org/man/virt-install.1)
* [Watchdog in Linux. JetHome.](https://docs.jethome.ru/en/controllers/linux/howto/watchdog.html)
