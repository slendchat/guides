Go to https://kernel.ubuntu.com/mainline/
choose the version you need.
also before installing check if there is enough space on `/boot` partition
download
```
linux-modules-6.14.0-061400-generic_6.14.0-061400.202503241442_amd64.deb
linux-image-unsigned-6.14.0-061400-generic_6.14.0-061400.202503241442_amd64.deb	
linux-headers-6.14.0-061400-generic_6.14.0-061400.202503241442_amd64.deb
linux-headers-6.14.0-061400_6.14.0-061400.202503241442_all.deb
```

in directory where downloaded these files run
```
sudo dpkg -i linux-*.deb 
```

then check if everything installed correctly
and
```
sudo update-grub
sudo reboot now
```

Если ты просто тестируешь новое ядро (например, 6.14 от Canonical), `unsigned` — норм.  
Если система с UEFI + Secure Boot, и ты хочешь чтобы ядро грузилось без танцев — ставь `signed`.

then delete old versions of kernel
list all packages corresponding to linux kernel with
`dpkg --list | egrep -i --color 'linux-image|linux-headers|linux-modules' | awk '{ print $2 }'`

then 
`sudo apt purge [the list of kernels]`
example:
```
sudo apt purge linux-headers-6.14.0-061400-generic \
linux-headers-6.8.0-54 \
linux-headers-6.8.0-54-generic \
linux-headers-6.8.0-57 \
linux-headers-6.8.0-57-generic \
linux-headers-generic \
linux-image-6.8.0-53-generic \
linux-image-6.8.0-54-generic \
linux-image-6.8.0-57-generic
```

