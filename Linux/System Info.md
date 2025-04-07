# System Info (kernel os)

- To get info about operating system
`cat /etc/*release`
Example:
```
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=24.04
DISTRIB_CODENAME=noble
DISTRIB_DESCRIPTION="Ubuntu 24.04.1 LTS"
PRETTY_NAME="Ubuntu 24.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.1 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
```

- To get info about system
`hostnamectl`
Example:
```
 Static hostname: vm1usm
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: b21f0dc0dc7949d6b9d8d568b63fbd31
         Boot ID: cfc27d92f64349a6ab41cd832e3b7b4b
  Virtualization: vmware
Operating System: Ubuntu 24.04.1 LTS
          Kernel: Linux 6.8.0-57-generic
    Architecture: x86-64
 Hardware Vendor: VMware, Inc.
  Hardware Model: VMware Virtual Platform
Firmware Version: 6.00
   Firmware Date: Thu 2020-11-12
    Firmware Age: 4y 4month 3w 3d
```

- Info about kernel
`uname -r`
Example:
`6.8.0-57-generic`

- debian/ubuntu
`dpkg -l | grep linux-image`

|Статус|Пакет|Версия|Архитектура|Комментарий|
|---|---|---|---|---|
|`rc`|`linux-image-6.8.0-53-generic`|6.8.0-53.55|amd64|**Удалён, но остались конфиги**|
|`ii`|`linux-image-6.8.0-54-generic`|6.8.0-54.56|amd64|**Установлен и активен**|
|`ii`|`linux-image-6.8.0-57-generic`|6.8.0-57.59|amd64|**Установлен, возможно, текущий**|
|`ii`|`linux-image-generic`|6.8.0-57.59|amd64|**Мета-пакет** (указывает на последнее стабильное ядро)|


### Info CPU, RAM, HDD
`lscpu`, `free -h`, `lsblk`, `df -h`, `inxi -Fxz`

- `lscpu` - CPU details
- `free -h` - RAM and swap usage
- `lsblk` - Disks and partitions
- `df -h` - Mounted filesystems usage
- `inxi -Fxz` - Full system overview (hardware + software)

### Dmesg, journalctl
- `dmesg | less` — сообщения ядра
- `journalctl -b` — логи текущей загрузки

### Uptime, users
- `uptime`, `who`, `w`, `last`