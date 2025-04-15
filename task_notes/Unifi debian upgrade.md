1. Set Apt sources.list for debian 9 `/etc/apt/sources.list`
```
deb http://archive.debian.org/debian/ stretch main contrib non-free
```

2. Install python 3.6 following this guide:
https://monovm.com/blog/how-to-install-python3-on-debian9/

3. Add superadmin to unifi mongo database
```
wget https://raw.githubusercontent.com/HostiFi/support-tools/main/lib/unifi/py/create-super-admin.py
```

 run it:
```
python3 create-super-admin.py -u Artur.Mamaliga -p Stager123# -e Artur.Mamaliga@eximbank.com
```


4. upgrade Debian 9 to the latest version
```
apt update
apt upgrade
apt dist-upgrade
apt full-upgrade
```
reboot

5. Download unifi upgrade script and run it.
```
apt-get update; apt-get install ca-certificates curl -y
```

```
curl -sO https://get.glennr.nl/unifi/update/unifi-update.sh && bash unifi-update.sh
```

Select `[4]`

6. Check everything

7. Upgrade debian to version 10
change `/etc/apt/sources.list`

```
deb http://archive.debian.org/debian/ buster main contrib non-free
```

8. upgrade to Debian 10
```
apt update
apt upgrade
apt dist-upgrade
apt full-upgrade
```
reboot

9. Upgrade to debian 11 
