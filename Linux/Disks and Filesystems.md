## **Ext4**

Самая популярная ФС на линукс. 
**Advantages**:
- High performance for most workloads.
- Reliable journaling, reducing the risk of data corruption after system crashes.
- Supports large file and partition sizes.
## **Btrfs**

Современнее ext4, It offers features such as snapshot support, data deduplication, RAID, and online defragmentation. Btrfs also enables the user to expand or shrink file systems on-the-fly, making it a flexible choice for both single and multi-disk setups.
**Advantages**:
- Built-in data integrity with checksums.
- Efficient space usage through data compression and deduplication.
- Snapshots for easy system backups and recovery.
## **XFS**

Более серверная ФС, лучше работает с большими объемами данных.
**Advantages**:
- Efficient handling of large files and file systems.
- Excellent performance for parallel I/O operations.
- Robust journaling for data protection.
## **F2FS

F2FS is optimized for use with flash-based storage devices like SSDs and eMMC.
It aims to minimize write amplification and extend the lifespan of flash storage by reducing unnecessary writes.
**Advantages**:
- Efficient wear leveling for flash storage.
- Improved performance on flash-based devices.
- Reduced write overhead, leading to longer flash storage life.
### Основное:
- **/dev/sdX** — устройство диска (`X = a, b, c...`)
- **/dev/sdXN** — раздел на диске (`N = 1, 2, 3...`)
- **nvme0n1** - 0 номер контроллера, 1 номер диска (если будет 2 nvme то будет nvme0n2)
- **nvme0n1p1** - p1, p2 указывает на раздел
- Разделы бывают (MBR):
    - **Primary (основные)** – до 4 шт.
    - **Extended (расширенный)** – 1 шт. вместо primary, содержит логические
    - **Logical (логические)** – внутри extended

### Таблицы разделов:
- **MBR (MSDOS)** — старая, до 2 ТБ, до 4 primary
- **GPT** — современная, до 9.4 ZB, до 128 разделов, требуется для UEFI

### Инструменты:
- `fdisk` — для MBR
- `gdisk` — для GPT
- `parted` или `gparted` — универсальные

### Полезные команды:

```
lsblk           # показывает диски и разделы 
fdisk -l        # подробный вывод по MBR-дискам 
parted -l       # для GPT 
blkid           # UUID и типы ФС
```

## LVM

scanning the system for block devices that LVM can access and manage.
```
sudo lvmdiskscan
```

To create physical volume
```
sudo pvcreate /dev/sda /dev/sdb
```

Output 
  Physical volume "/dev/sda" successfully created

```
sudo pvs
```
Output
  PV              VG             Fmt     Attr   PSize      PFree
  /dev/sda3  ubuntu-vg lvm2   a--    18.22g    0

Create a volume group.
Most of the time, you only have a single volume group per system for maximum flexibility in allocation.
```
sudo vgcreate LVMVolGroup /dev/sda 
```

The following command adds the physical volume `/dev/sdf1` to the volume group `vg1`.
```
vgextend LVMVolGroup /dev/sda
```

To create logical volumes, use the `lvcreate` command.
```
sudo lvcreate -L 10G -n projects LVMVolGroup
sudo lvcreate -L 5G -n www LVMVolGroup
sudo lvcreate -L 20G -n db LVMVolGroup
```

You can view the logical volumes and their relationship to the volume group by selecting a custom output from the `vgs` command:
```
sudo vgs -o +lv_size,lv_name
```

Command to create workspace volume using `-l` flag occupying 100%FREE space
```
sudo lvcreate -l 100%FREE -n workspace LVMVolGroup
```

To format your four logical volumes with the Ext4 filesystem, run the following commands:

```
sudo mkfs.ext4 /dev/LVMVolGroup/projects
sudo mkfs.ext4 /dev/LVMVolGroup/www
sudo mkfs.ext4 /dev/LVMVolGroup/db
sudo mkfs.ext4 /dev/LVMVolGroup/workspace
```





> ![[LVM_scheme.png]]