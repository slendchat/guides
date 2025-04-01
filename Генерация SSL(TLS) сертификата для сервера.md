CN (Common Name) - это основное имя, на которое будет выдан сертификат.  
Обычно — домен
Также необходим SAN (Subject Alternative Name)
Это расширение, которое указывает дополнительные домены и IP, на которые тоже действителен сертификат.
SAN необходим, так как современные браузеры не примут подключение по https с сертификатом без SAN.

Этапы выдачи сертифика веб-серверу:
Генерация CSR файла (Certificate Signing Request), удобно перед этим создать конфигурационный файл для генерации CSR.
## 1. CSR and .cnf file

`yourdomain.cnf`:
```
[ req ]
default_bits       = 2048
default_md         = sha256
prompt             = no
distinguished_name = req_distinguished_name
req_extensions     = req_ext

[ req_distinguished_name ]
C  = MD
ST = Chisinau
L  = Chisinau
O  = Organization
OU = Organizational unit
CN = yourdomain.com
emailAddress = admin@yourdomain.com

[ req_ext ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = yourdomain.com
DNS.2 = www.yourdomain.com
IP.1  = 192.168.0.1
IP.2  = 192.168.0.2
```


