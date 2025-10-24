На 3750G IP не назначается на физический порт, а на интерфейс VLAN.
пример:
```
interface vlan 1
ip address 192.168.1.128 255.255.255.0
ip default-gateway 192.168.1.1
no shutdown
```

