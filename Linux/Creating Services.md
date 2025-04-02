This guide is about creating services on Linux with systemd as init system

### 1. Define the service

```
sudo vim /etc/systemd/system/my_service.service
```

to write those service unit files you can address man page of systemd
https://www.google.com/search?q=systemd&sitesearch=man7.org%2Flinux%2Fman-pages&sa=Search+online+pages
https://man7.org/linux/man-pages/man5/systemd.service.5.html

Here is the basic template:
```
[Unit]  
Description=My Custom Service  
After=network.target  
  
[Service]  
ExecStart=/path/to/your/executable  
Restart=always  
User=your_username  
Group=your_groupname  
Environment=VAR_NAME=var_value  
  
[Install]  
WantedBy=default.target
```
