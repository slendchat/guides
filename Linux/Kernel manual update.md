Go to https://kernel.ubuntu.com/mainline/
choose the version you need.
download
```
linux-modules-6.14.0-061400-generic_6.14.0-061400.202503241442_amd64.deb
linux-image-unsigned-6.14.0-061400-generic_6.14.0-061400.202503241442_amd64.deb	
linux-headers-6.14.0-061400-generic_6.14.0-061400.202503241442_amd64.deb
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
