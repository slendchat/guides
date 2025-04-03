# Обзор
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

---

# Форматирование и создание ФС

Команда `mkfs` - для форматирования разделов и томов (создания файловой системы)
#### Общая структура команды:
```
mkfs -t <тип_фс> [опции] <устройство>
```
или напрямую
```
mkfs.ext4 /dev/sdX1
```

#### Поддерживаемые типы ФС и команды:

|Тип ФС|Команда|Комментарий|
|---|---|---|
|ext2|`mkfs.ext2`|Устаревшая, без журналирования|
|ext3|`mkfs.ext3`|С журналом, но уже редко используется|
|ext4|`mkfs.ext4`|Основная ФС для Linux|
|xfs|`mkfs.xfs`|Хороша для больших файлов и систем|
|btrfs|`mkfs.btrfs`|Современная, с snapshot'ами|
|f2fs|`mkfs.f2fs`|Оптимизирована для флеш-памяти|
|vfat|`mkfs.vfat` или `mkfs.fat`|Для флешек, совместима с Windows|
|ntfs|`mkfs.ntfs` (через `ntfs-3g`)|Используется редко, нужно ставить пакет|

Порядок операций при форматировании и создании ФС
1. Проверить что диск не смонтирован
```
umount /dev/sdX1
```
2. Очистить раздел (опционально)
```
wipefs -a /dev/sdb1   # удаляет сигнатуры ФС
```
3. Отформатировать и создать файловую систему
```
mkfs.btrfs -L btrfs_store /dev/sdb1 # -L метка тома
```
4. Смонтировать созданную ФС
```
mount /dev/sdX1 /mnt/mydata
```



---
# LVM

![[LVM_scheme.png]]

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

After formatting, create mount points:
```
sudo mkdir -p /mnt/{projects,www,db,workspace}
```

Then mount the logical volumes to the appropriate location:
```
sudo mount /dev/LVMVolGroup/projects /mnt/projects
sudo mount /dev/LVMVolGroup/www /mnt/www
sudo mount /dev/LVMVolGroup/db /mnt/db
sudo mount /dev/LVMVolGroup/workspace /mnt/workspace
```

### Summary

#### Типовой процесс:
```
# Инициализация физического тома
pvcreate /dev/sdX

# Создание группы томов
vgcreate my_vg /dev/sdX

# Создание логического тома
lvcreate -L 10G -n my_lv my_vg

# Форматирование и монтирование
mkfs.ext4 /dev/my_vg/my_lv
mount /dev/my_vg/my_lv /mnt/mydata
```

#### Расширение тома
```
lvextend -L +5G /dev/my_vg/my_lv
resize2fs /dev/my_vg/my_lv                # если ext4
xfs_growfs /mnt/mydata                    # если xfs Только онлайн-расширение
btrfs filesystem resize max /mnt/mydata   # если btrfs
f2fs_resize /dev/my_vg/my_lv              # если f2fs Только онлайн-расширение
```
#### Проверка
```
pvs     # физ. тома
vgs     # группы
lvs     # лог. тома
```

#### Уменьшение тома с **ext4**

1. **Отключи монтирование**:
```bash
umount /dev/my_vg/my_lv
```

2. **Проверь ФС на ошибки (обязательно)**:
```bash
e2fsck -f /dev/my_vg/my_lv
```

3. **Уменьши файловую систему**:
```bash
resize2fs /dev/my_vg/my_lv 10G   # новое значение размера
```

4. **Теперь уменьшай сам том**:
```bash
lvreduce -L 10G /dev/my_vg/my_lv
```

5. **Снова смонтируй**:
```bash
mount /dev/my_vg/my_lv /mnt/mydata
```

#### Уменьшение тома с **btrfs**

Btrfs поддерживает **уменьшение** _только если_ ФС **смонтирована**.

1. **Просто укажи меньшее значение**:
```bash
btrfs filesystem resize -5G /mnt/mydata   # уменьшить на 5ГБ
```

или:
```bash
btrfs filesystem resize 20G /mnt/mydata   # установить точный размер
```

2. **Проверь результат**:
```bash
btrfs filesystem show /mnt/mydata
```

📌 **Важно:**
- У ext4 сначала уменьшается ФС, потом LV.
- У btrfs наоборот — сначала LV (если используешь LVM), потом btrfs, и всё это можно делать онлайн.

