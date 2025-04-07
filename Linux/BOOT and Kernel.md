
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


