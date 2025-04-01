CN (Common Name) - это основное имя, на которое будет выдан сертификат.  
Обычно — домен
Также необходим SAN (Subject Alternative Name)
Это расширение, которое указывает дополнительные домены и IP, на которые тоже действителен сертификат.
SAN необходим, так как современные браузеры не примут подключение по https с сертификатом без SAN.

Этапы выдачи сертифика веб-серверу:
Генерация CSR файла (Certificate Signing Request), удобно перед этим создать конфигурационный файл для генерации CSR.
## 1. CSR and .cnf file
CN = main name for certificate
alt_names = other names for server (IP addr, subdomains, etc.)
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

## 2. Generating Private Key and CSR file

```
openssl req -new -nodes -newkey rsa:2048 \
-keyout yourdomain.key \
-out yourdomain.csr \
-config yourdomain.cnf
```

## 3. Signing cert on root CA

Go to http://domain_serv/certsrv/
`Request Certificate` -> `advanced certificate request` -> {
	1. Paste CSR content to the `Base-64-encoded certificate request`
	2. Certificate Template - web server
	3. Base64 encoded
	4. Download certificate chain
}

## 4. Put the certificate on server
Copy the chain certificate to server and connect it to Apache or Nginx
or move to default directory for trusted Certs, but this is another topic.

## 5. Explanation of certificates

> ![[certs_tree.png]]

### X.509
- Это стандарт сертификатов.
- Определяет структуру сертификата: **issuer, subject, CN, SAN, public key, signature** и т.д.

### Base64 ASCII (текстовые)

#### **PEM (Privacy-Enhanced Mail)**
- Расширения: `.pem`, `.crt`, `.cer`, `.key`
- **ASCII-кодировка Base64**
- Содержимое между:
```
	-----BEGIN CERTIFICATE----- 
	 (Certificate)
	-----END CERTIFICATE-----
```

- Часто используется в **Linux**, **Apache**, **Nginx**.
- Может содержать:
    - Сертификат
    - Приватный ключ
    - Цепочку сертификатов

####  **PKCS#7**
- Расширения: `.p7b`, `.p7c`
- **Base64**
- Только **сертификаты**, **без приватного ключа**
- Часто используется в **Windows**, **Java (Tomcat)**

---

###  Binary (бинарные)
#### **DER (Distinguished Encoding Rules)**
- Расширения: `.der`, `.cer`
- **Бинарный формат**
- Тот же X.509, но в бинаре.
- Часто используется в **Java**, **Windows**
#### **PKCS#12**
- Расширения: `.pfx`, `.p12`
- **Бинарный**
- Содержит **сертификат + цепочку + приватный ключ**
- **Пароль-защищённый**
- Используется в **Windows**, **IIS**, **Mac**, **Browsers (импорт/экспорт)**