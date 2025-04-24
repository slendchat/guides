# Output current time
Check current time `timedatectl`
- **Local time**
	**Описание:** Локальное системное время, отображаемое с учётом текущего часового пояса.

- **Universal time (UTC)**
	**Описание:** Универсальное координированное время (UTC), независимое от часовых поясов.

- **RTC time**
	**Описание:** Время аппаратных (материнских) часов — Real-Time Clock (RTC).  

- **Time zone**
	**Описание:** Установленный системный часовой пояс.

- **System clock synchronized**
	**Описание:** Состояние синхронизации системного времени с сервером точного времени.

- **NTP service**
	**Описание:** Информация о сетевом сервисе времени (например, systemd-timesyncd или chronyd).

- **RTC in local TZ**
	**Описание:** Указывает, используется ли локальный часовой пояс для RTC.

Example:
```
               Local time: Mon 2025-04-14 09:01:25 EEST
           Universal time: Mon 2025-04-14 06:01:25 UTC
                 RTC time: Mon 2025-04-14 06:01:25
                Time zone: Europe/Chisinau (EEST, +0300)
System clock synchronized: no
              NTP service: n/a
          RTC in local TZ: no
```

# Time synchronization with NTP
## Connecting
Чтобы синхронизировать время, используют демон **ntpd**

Install NTP package
```bash
sudo apt install ntp
```

**driftfile /var/lib/ntp/ntp.drift.** В ней указан файл, в котором хранится информация о том, как часто смещается время. В этом же файле содержится и значение, которое было получено из предыдущих изменений времени. 
Файл, в котором `ntpd` хранит информацию об отклонении системных часов.
Позволяет NTP сохранять точность между перезагрузками.

Логи синхронизации – **logfile /var/log/ntp.log**.

Configure NTP servers to use, the config is in file `/etc/ntp.conf`
Change or comment default configuration:
```
pool 0.debian.pool.ntp.org iburst
pool 1.debian.pool.ntp.org iburst
pool 2.debian.pool.ntp.org iburst
pool 3.debian.pool.ntp.org iburst
```
These are DNS round-robin addresses.

- `pool` - tells `ntpd` to sync time with a **group of public NTP server**
- `server`  - connect to a single NTP server
- `prefer` - preferred NTP server 

Через опцию **iburst** можно увеличить точность синхронизации, то есть указать то, что на сервер необходимо отправлять несколько пакетов (4-8) вместо одного.

## Access rules
`restrict` - rules of access control
  Format:
```
restrict <ip/net> [mask <subnet>] [options...]
```

Examples:
```
restrict -4 default kod notrap nomodify nopeer noquery
restrict 127.0.0.1
restrict ::1
restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap
```

|Параметр|Назначение|
|---|---|
|`-4`|Ограничение только на IPv4|
|`default`|Применяется ко всем IP, если не указано иное|
|`kod`|"Kiss-o'-Death" — если нарушают политику, отправить отказ|
|`notrap`|Не разрешать установку событийных ловушек (не используется почти нигде)|
|`nomodify`|Запрет изменять настройки сервера|
|`nopeer`|Запрет устанавливать симметричную ассоциацию|
|`noquery`|Запрет всех запросов на чтение (например, `ntpq`)|
|`restrict 127.0.0.1`|Локальной машине доступ разрешён|
|`restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap`|К локальной сети — разрешён доступ без права модификации|

## Tips
Public NTP pools
- Азия – asia.pool.ntp.org
- Европа – europe.pool.ntp org
- Африка – africa.pool.ntp.org
- Северная Америка – north-america.pool.ntp.org
- Южная Америка – south-america.pool.ntp.org
- Океания – oceania.pool.ntp.org
- Россия – ru.pool.ntp.org

## Apply new NTP rules

After saving configuration in `/etc/ntp.conf`
Restart the service:
```
systemctl restart ntp
```

 shows the **list of NTP peers** your system is connected or trying to.
```
ntpq -p
```

- remote – адрес сервера точного времени;
- refid – вышестоящий сервер;
- st – уровень (stratum) сервера;
- t – тип пира (u- unicast, m- multicast);
- when – время последней синхронизации;
- poll – время в секундах, за которое демон NTP синхронизируется с пиром;
- reach – состояние доступности сервера;
- delay – время задержки ответа от сервера;
- offset – временная разница между сервером и сервером синхронизации;
- jitter – смещение времени на удаленном сервере.

Слева от адреса сервера могут быть указаны еще и такие символы:

- * – сервер выбран для синхронизации;
- + – сервер, пригодный для синхронизации;
- – – с сервером синхронизироваться не стоит;
- х – сервер недоступен.

Чтобы проверить, насколько сервер подходит для синхронизации, нужно использовать команду `ntpdate -q`


# Timesyncd

`timedatectl status` retunr
