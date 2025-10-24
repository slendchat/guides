1. create a new group and select a security model
```
configure terminal
snmp-server enable traps
snmp-server engineID local <engine-id>
snmp-server group <group-name> v3 priv
snmp-server user <username> <group-name> v3 auth sha <auth-password> priv aes 128 <priv-password>
snmp-server host <host-ip> version 3 auth <username>
```

Explanation