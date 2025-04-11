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
