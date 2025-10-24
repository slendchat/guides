1. create a new group and select a security model
```
configure terminal
snmp-server enable traps
snmp-server engineID local <engine-id>
snmp-server group <group-name> v3 priv
snmp-server user <username> <group-name> v3 auth sha <auth-password> priv aes 128 <priv-password>
snmp-server host <host-ip> version 3 auth <username>
end
write memory
```

Explanation
1. `configure terminal`
Включение конфигурационного режима

2. `snmp-server enable traps`
Эта команда включает **отправку SNMP traps** (уведомлений) на заранее указанные хосты.  
Т.е. устройство будет **само отправлять сообщения** SNMP-менеджеру (например, о падении интерфейса, смене статуса и т.д.)

Можно дополнительно уточнить типы trap-ов:
```
snmp-server enable traps syslog 
snmp-server enable traps linkdown linkup
```
без аргументов — включает все стандартные.

3. `snmp-server engineID local <engine-id>`
Задаёт **уникальный идентификатор SNMP Engine ID** для локального устройства.
SNMPv3 использует Engine ID как "уникальный отпечаток" устройства.
Он участвует в генерации аутентификационных ключей и идентификации агента.
Обычно Cisco генерирует его сама (на основе MAC-адреса или IP)
Но если ты хочешь, чтобы ключи совпадали при восстановлении конфигурации (например, при замене роутера), можно задать вручную.

Можно не использовать.

4. `snmp-server group <group-name> v3 priv`
Создаёт **группу безопасности SNMPv3** с именем `<group-name>`.
- `<group-name>` - произвольное имя (например, `SNMPAdmins`)
- `v3` - указывает версию SNMP
- `priv` - уровень безопасности (security level)
`noauth` - Без аутентификации и шифрования
`auth` - Есть аутентификация, нет шифрования
`priv` - Есть и аутентификация, и шифрование

4. `snmp-server user <username> <group-name> v3 auth sha <auth-password> priv aes 128 <priv-password>`
- `<username>` — имя пользователя SNMP (например, `monitor`)
- `<group-name>` — имя группы (например, `SNMPAdmins`, должно совпадать с тем, что в предыдущей команде)
- `v3` — версия SNMP
- `auth sha <auth-password>` — тип аутентификации и пароль
    - `auth` — включает проверку подлинности
    - `sha` — алгоритм (можно также `md5`, но SHA надёжнее)
    - `<auth-password>` — пароль для аутентификации
- `priv aes 256 <priv-password>` — включает шифрование (privacy)
    - `aes 256` — алгоритм шифрования (можно также `des`, `3des`, `aes 192`, `aes 256`)
    - `<priv-password>` — пароль для шифрования

4. `snmp-server host <host-ip> version 3 auth <username>`
Настраивает **куда** Cisco будет отправлять traps.
- `<host-ip>` — IP SNMP-менеджера (например, 192.168.1.100)
- `version 3` — SNMPv3
- `auth` — уровень безопасности (можно `noauth`, `auth`, `priv`, но чаще `auth`)
- `<username>` — имя пользователя SNMPv3, созданного ранее (он будет использоваться для trap-аутентификации)

