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
User=your_username  
Group=your_groupname  
Environment=VAR_NAME=var_value  
Restart=on-failure
  
[Install]  
WantedBy=multi-user.target
```

Explanation:

- `[Unit]`: Descriptive information and dependencies.  
- `[Service]`: Execution details, such as the command to start the service.  
- `[Install]`: Specifies where the service should be linked.

 `[Unit]`
- `Description`: Human-readable name.
- `After`: Defines ordering. E.g., `network.target` ensures network is up.
`[Service]`
- `Type`:
    - `simple` (default): just run the command.
    - `forking`: for daemons that fork.
    - `oneshot`: for scripts that do one task and exit.
- `User`: run the service as this user.
- `ExecStart`: what to run.
- `Restart`: handle restarts (e.g., `always`, `on-failure`, `no`).
`[Install]`
- `WantedBy=multi-user.target` makes it start at boot 

### 2. Reload and apply the service

reload the systemd configuration, to make it recognize the new service.
```
sudo systemctl daemon-reload
```

then Enable and Start the Service
```
sudo systemctl enable my_service
sudo systemctl start my_service
```
