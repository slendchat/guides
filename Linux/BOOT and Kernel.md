
Grub main configuration file is located at `/boot/grub/grub.cfg`, but you shouldn't edit it.

Grub settings that can be changed are located at `/etc/default/grub`

Scripts and themes for grub are also located in the `/etc/grub.d/`. There's also an os-prober script that checks the system's internal hard drives for other installed operating systems—Windows, other Linux distributions

Grub configuration is created by running the `update-grub` or `grub2-mkconfig` - combining files from 
`/etc/default/grub` + `/etc/grub.d/`