Отлично, Artur, ты всё делаешь по классике 💪 Осталось только упаковать это в **Ansible playbook**. Вот тебе готовый рабочий плейбук, который можно катать по всем Ubuntu-машинам.

---

## 📁 Структура (если хочешь по папкам):

```
node_exporter/
├── files/
│   └── node_exporter-<версия>.linux-amd64.tar.gz
├── tasks/
│   └── main.yml
├── templates/
│   └── node_exporter.service.j2
└── playbook.yml
```

---

## 🔧 `playbook.yml`

```yaml
- hosts: all
  become: yes
  tasks:
    - include_tasks: tasks/main.yml
```

---

## 📜 `tasks/main.yml`

```yaml
- name: Create node_exporter user
  user:
    name: node_exporter
    shell: /usr/sbin/nologin
    system: yes
    create_home: no

- name: Copy node_exporter archive
  copy:
    src: node_exporter-1.7.0.linux-amd64.tar.gz
    dest: /tmp/

- name: Extract node_exporter
  unarchive:
    src: /tmp/node_exporter-1.7.0.linux-amd64.tar.gz
    dest: /tmp/
    remote_src: yes

- name: Move node_exporter binary
  copy:
    src: /tmp/node_exporter-1.7.0.linux-amd64/node_exporter
    dest: /usr/bin/node_exporter
    mode: '0755'
    owner: node_exporter
    group: node_exporter
    remote_src: yes

- name: Create systemd service
  template:
    src: node_exporter.service.j2
    dest: /etc/systemd/system/node_exporter.service

- name: Reload systemd
  command: systemctl daemon-reexec

- name: Enable and start node_exporter
  systemd:
    name: node_exporter
    enabled: yes
    state: started
```

---

## ⚙️ `templates/node_exporter.service.j2`

```ini
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/bin/node_exporter

[Install]
WantedBy=default.target
```

---

## ✅ Что ты получишь:

- Создан системный юзер `node_exporter`
    
- Файл положен в `/usr/bin`
    
- Запущен systemd сервис
    
- Автозапуск при старте системы
    

---

Можешь гонять этот Ansible по группе машин, и всё будет красиво. Хочешь — могу добавить таску, чтобы сам качал `.tar.gz` с GitHub — без ручного скачивания.