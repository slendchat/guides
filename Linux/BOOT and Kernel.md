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

---

# System Info

To get info about operating system
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

To get info about system
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

