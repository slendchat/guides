
It is said that debian has a large support for major version update
here's the step by step guide on how to do this:
## 1. Backup data
For example take a snapshot of the VM.
## 2. Check if `/boot/` directory has space for new kernel
The size of the latest Linux kernel is approximately 200-250 MB  
## 3. Update ALL existing installed packages corresponding to current version
```
sudo apt update  
sudo apt upgrade  
sudo apt dist-upgrade  
sudo apt --purge autoremove #if u want to delete old packages
```

## 4. Reboot to apply kernel and other updates corresponding to current version.
```
sudo reboot
```
## 5. Reconfigure APT’s source-list files
What is a source list file?
Each line tells APT:
> “Here’s where to find packages, and what kind.”

Basic syntax:
`deb [options] http://mirror/url distribution component1 component2 ...`

Example:
`deb http://deb.debian.org/debian stretch main contrib non-free`

Breakdown:
- `deb` – means binary packages (most cases)
- `deb-src` – means source packages (optional)
- `http://...` – the URL of the mirror/repo
- `stretch` – the **codename** of the release
- `main contrib non-free` – repository **components**:
    - `main` – free/open-source packages
    - `contrib` – free packages that depend on non-free stuff
    - `non-free` – closed source, proprietary (e.g. firmware)

> ⚠️ Since Debian 9 is archived, regular mirrors won’t work — you need to use `archive.debian.org`.

- Debian 6 Squeeze
- Debian 7 Wheezy
- Debian 8 Jessie
- Debian 9 Stretch
- Debian 10 Buster
**Current LTS Release(s)**
- Debian 11 Bullseye
**Future LTS Release(s)**
- Debian 12 Bookworm

Change current version name of debian in apt package list to newer one. Upgrade i safer when made by step equal to one major version, not two or three.
## 6. Apply changes
Run:
```
sudo apt update
sudo apt upgrade
```

Try to restart services if prompted and to keep local version installed of software if possible.

Then run:
```
sudo apt full-upgrade
sudo reboot
```

## 7. Verify and clean
Verify the update by running:
```
uname -r  
lsb_release -a
```

Additionally you can clean the os from outdated and unused packages
```
sudo apt --purge autoremove
```

source: https://www.cyberciti.biz/faq/update-upgrade-debian-9-to-debian-10-buster/