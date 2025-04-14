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
Install NTP package
```bash
sudo apt install ntp
```

Configure NTP servers to use, the config is in file `/etc/ntp.conf`
Change or comment defau
