
It is said that debian has a large support for major version update
here's the step by step guide on how to do this:
1. Back up data
2. Check if `/boot/` directory has space for new kernel
3. Update ALL existing installed packages corresponding to current version
```
sudo apt update  
sudo apt upgrade  
sudo apt dist-upgrade  
sudo apt --purge autoremove #if u want to delete old packages
```

4. Reboot to apply kernel and other updates corresponding to current version.
`sudo reboot`
5. Reconfigure APT’s source-list files









source: https://www.cyberciti.biz/faq/update-upgrade-debian-9-to-debian-10-buster/