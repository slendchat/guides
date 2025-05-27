## ✅ **ЭТАП 0: Подготовка**

📋 У тебя должен быть:

- Доменный пользователь `EXIMBANK\script-runner`
    
- Список Windows-хостов (по IP или DNS)
    
- Установленный PowerShell на хостах (по умолчанию есть)
    
- Ansible-контроллер с `pywinrm`
    

---

## 🧩 **ЭТАП 1: Проверка и добавление пользователя в группу**

### 📌 Цель: дать права на удалённый доступ

На **каждом хосте**, от имени администратора:

```powershell
$domainUser = "EXIMBANK\script-runner"
$group = "Remote Management Users"

# Проверим, есть ли уже
if (-not (Get-LocalGroupMember -Group $group -Member $domainUser -ErrorAction SilentlyContinue)) {
    Add-LocalGroupMember -Group $group -Member $domainUser
    Write-Host "✅ Добавлен $domainUser в группу $group"
} else {
    Write-Host "ℹ️ Уже состоит в $group"
}
```

---

## 🔐 **ЭТАП 2: Создание HTTPS сертификата и listener'а**

Твой скрипт — 🔥, просто вставь его в PowerShell и выполни от администратора:

```powershell
# === Start Script ===

# 1. Создание самоподписанного сертификата
$certParams = @{
    CertStoreLocation = 'Cert:\LocalMachine\My'
    DnsName           = $env:COMPUTERNAME
    NotAfter          = (Get-Date).AddYears(1)
    Provider          = 'Microsoft Software Key Storage Provider'
    Subject           = "CN=$env:COMPUTERNAME"
}
$cert = New-SelfSignedCertificate @certParams

# 2. Создание HTTPS WinRM listener
$httpsParams = @{
    ResourceURI = 'winrm/config/listener'
    SelectorSet = @{
        Transport = "HTTPS"
        Address   = "*"
    }
    ValueSet = @{
        CertificateThumbprint = $cert.Thumbprint
        Enabled               = $true
    }
}
New-WSManInstance @httpsParams

# 3. Открытие порта 5986
$firewallParams = @{
    Action      = 'Allow'
    Description = 'Inbound rule for Windows Remote Management via WS-Management. [TCP 5986]'
    Direction   = 'Inbound'
    DisplayName = 'Windows Remote Management (HTTPS-In)'
    LocalPort   = 5986
    Profile     = 'Any'
    Protocol    = 'TCP'
}
New-NetFirewallRule @firewallParams

# === End Script ===
```

---

## 📡 **ЭТАП 3: Проверка настройки WinRM**

На том же хосте:

```powershell
winrm enumerate winrm/config/listener
```

Убедись, что видишь **HTTPS Listener** с `CertificateThumbprint` и портом 5986.

---

## ⚙️ **ЭТАП 4: Ansible Inventory и Vault**

### 🔸 `inventory.ini`:

```ini
[windows]
winhost1.eximbank.local

[windows:vars]
ansible_connection=winrm
ansible_port=5986
ansible_winrm_transport=ntlm
ansible_winrm_scheme=https
ansible_winrm_server_cert_validation=ignore
ansible_user=EXIMBANK\\script-runner
ansible_password={{ vault_winrm_password }}
```

---

### 🔸 `vault.yml`:

```bash
ansible-vault create vault.yml
```

Добавь:

```yaml
vault_winrm_password: "StrongPassword123!"
```

---

## 🧪 **ЭТАП 5: Тестирование подключения**

```yaml
---
- name: Test Windows WinRM over HTTPS
  hosts: windows
  vars_files:
    - vault.yml
  tasks:
    - name: Check connection
      win_ping:
```

Запуск:

```bash
ansible-playbook test.yml -i inventory.ini --ask-vault-pass
```


