# BOOT - GRUB
Grub main configuration file is located at `/boot/grub/grub.cfg`, but you shouldn't edit it.

Grub settings that can be changed are located at `/etc/default/grub`

Scripts and themes for grub are also located in the `/etc/grub.d/`. There's also an os-prober script that checks the system's internal hard drives for other installed operating systems—Windows, other Linux distributions

Grub configuration is created by running the `update-grub` or `grub2-mkconfig` - combining files from 
`/etc/default/grub` + `/etc/grub.d/`

`GRUB_BADRAM=` - find out the use cases.

#### 1. **Edit GRUB default settings**
`sudo nano /etc/default/grub`
- This file contains variables that control GRUB's behavior like timeout, default OS, etc.

#### 2. **Set default boot entry**
`GRUB_DEFAULT=0`
- Sets the default boot option (index starts at 0).  
    Use `GRUB_DEFAULT=saved` to boot the last selected OS.

#### 3. **Enable last used boot entry**
`GRUB_DEFAULT=saved GRUB_SAVEDEFAULT=true`
- GRUB will remember your last selected OS and boot it next time.

#### 4. **Change GRUB timeout**
`GRUB_TIMEOUT=10`
- Time in seconds before default boot starts. Set to `0` to skip menu, `-1` to wait indefinitely.

#### 5. **Hide or show the GRUB menu**
`GRUB_HIDDEN_TIMEOUT=0`
- Set this to hide GRUB menu (deprecated in some distros).


#### 6. **Change GRUB resolution**
`GRUB_GFXMODE=1024x768`
- Sets graphical resolution for the GRUB menu.

#### 7. **Set a background image**
`GRUB_BACKGROUND="/boot/grub/mybackground.png"`
- Customizes the GRUB menu background.

#### 8. **Apply changes**
`sudo update-grub`
- Regenerates `/boot/grub/grub.cfg` with updated settings.


# Systemd boot process

`systemd-analyze` - system load time
Example:
```
Startup finished in 13.085s (kernel) + 22.082s (userspace) = 35.168s
graphical.target reached after 22.019s in userspace.
```

`systemd-analyze blame` — покажет **список юнитов**, отсортированный по времени запуска (что тормозит загрузку).
Example:
```
12.379s snap.docker.nvidia-container-toolkit.service
11.437s snapd.seeded.service
11.179s snapd.service
...
```

`systemctl status` — общая сводка состояния системы и systemd.

`systemctl list-units --failed` — список **упавших/неудачных** сервисов.
- useful to use after boot - it is clearly seen what didn't startup.

Compare systemd vs init.
- `systemd` is the modern init system (faster, parallel, better logging).
- `init` (SysV) is older (sequential, shell scripts).

# Partitions automount

`/etc/fstab` - file describes what drives and partitions should be mounted at boot.
```
cat /etc/fstab
# UUID=... /mnt/data ext4 defaults 0 2
```
For errors check `journalctl -b` or `mount -a`

Linux prefers to use `UUID` (**Universally Unique Identifier**), LABEL, or symlinks to identify media storage devices on a system

1. Create a directory where the disk will be mounted.
```
sudo mkdir /mnt/mnt1
```

In addition, I would make the user the owner and give him the right to read/write:
```
sudo chown [user]:[group] /media/Data
sudo chmod +rw /media/Data
```

2. Now the `fstab` entry.
- Install `libblkid1` to see device specific information:
```
sudo apt-get install libblkid1
 ```

- Enter `sudo blkid` to see UUID of disks
```
/dev/sda2: UUID="32a4b76f-246e-486e-8495-31b8a781fb4c" TYPE="swap" 
/dev/sda1: UUID="31f39d50-16fa-4248-b396-0cba7cd6eff2" TYPE="ext4"
```

- Then we create the `fstab` entry:
```
sudo vim /etc/fstab
```

and append the line:
```
UUID=31f39d50-16fa-4248-b396-0cba7cd6eff2 /mnt/mnt1 auto rw,user,auto 0 0
```

or
```
/dev/disk/by-uuid/1f5d1c67-9921-49df-a896-410526aa4df9 /media/Data ext4 defaults,auto 0 2
```
(and afterwards give a empty new line to avoid warnings).

| Поле                           | Значение                                                                                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. `/dev/disk/by-uuid/...`** | **Путь к разделу по UUID** (уникальный ID, лучше чем `/dev/sdX`, т.к. не меняется при перезагрузке).                                                          |
| **2. `/media/Data`**           | **Точка монтирования** — куда будет примонтирован раздел.                                                                                                     |
| **3. `ext4`**                  | **Файловая система** — здесь `ext4`.                                                                                                                          |
| **4. `defaults,auto`**         | **Опции монтирования**:  <br>- `defaults` — стандартные (rw, suid, dev, exec, auto, nouser, async)  <br>- `auto` — монтируется **автоматически при загрузке** |
| **5. `0`**                     | Используется для **дампа (резервного копирования)**. Почти всегда `0`.                                                                                        |
| **6. `2`**                     | **Порядок проверки `fsck`**:  <br>- `1` — для `/` (root)  <br>- `2` — для других разделов  <br>- `0` — не проверять                                           |


To mount the partition, open a terminal and run:

```
mount /mnt/mnt1
```

Because of the entry `auto` it should be mounted automatically on next boot.

Before the next boot, don't forget to verify the entries! On any error in the `fstab` file, the system will not start and you will need to recover it, by reverting the changes. You can verify the entries with:

```
sudo findmnt --verify
```


Utility named `grubby` is supported only on RHEL based destribution, ubuntu or debian does not support this.
