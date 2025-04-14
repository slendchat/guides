https://www.digitalocean.com/community/tutorials/how-to-install-lamp-stack-on-ubuntu

Install APACHE2
```
sudo apt install apache2
```

Optional configure firewall `ufw`
- **Apache**: This profile opens only port `80` (normal, unencrypted web traffic).
- **Apache Full**: This profile opens both port `80` (normal, unencrypted web traffic) and port `443` (TLS/SSL encrypted traffic).
- **Apache Secure**: This profile opens only port `443` (TLS/SSL encrypted traffic).
```
sudo ufw allow in "Apache"
```

Installing MySQL
```
sudo apt install mysql-server
```
When the installation is finished, it’s recommended that you run a security script that comes pre-installed with MySQL.
Start MySQL secure installation script
```
sudo mysql_secure_installation
```

Changing Root user password manually
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password123';
FLUSH PRIVILEGES;
```

Installing php with needed modules
```
sudo apt install php libapache2-mod-php php-mysql
```

## PHP.ini

List of directives - https://www.php.net/manual/en/ini.list.php

Commonly changed values are:
`;error_log = php_errors.log` -> `error_log = /var/log/php_errors.log`


- `memory_limit = 128M` - Limits how much **RAM a single PHP script** can use.
- `upload_max_filesize = 128M` - **Maximum file size** a user can upload via a form.
- `post_max_size = 128M` - Sets the max **total size of POST data** (form fields + files).
- `max_execution_time = 120` - Maximum **runtime in seconds** for a PHP script before it’s killed.


## Supervisor & supervisor.conf

Is a daemon that controls other services.
`supervisor.conf` is main config file that describes:
 - What programs to run.
 - Where to store logs.
 - Parameters like reloads, dirs and vars.
 - Controlls them (start/stop/restart)

Work with supervisor:
```
# start supervisord
sudo supervisord -c /etc/supervisord.conf

# process control
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl status
sudo supervisorctl restart myworker
```

Where config is stored:
- Ubuntu/Debian:
    - main conf: `/etc/supervisor/supervisord.conf`
    - other programs: `/etc/supervisor/conf.d/*.conf`
- CentOS/Alma:
    - `/etc/supervisord.conf` or `/etc/supervisord.d/`

Supervisor.conf example:

```
[supervisord]
nodaemon=true
logfile=/dev/null
user=root

# apache2
[program:apache2]
command=/usr/sbin/apache2ctl -D FOREGROUND
autostart=true
autorestart=true
startretries=3
stderr_logfile=/proc/self/fd/2
user=root

# mariadb
[program:mariadb]
command=/usr/sbin/mariadbd --user=mysql
autostart=true
autorestart=true
startretries=3
stderr_logfile=/proc/self/fd/2
user=mysql
```