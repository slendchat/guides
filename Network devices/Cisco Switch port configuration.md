На 3750G IP не назначается на физический порт, а на интерфейс VLAN.
пример:
```
interface vlan 10
ip address 10.103.1.128 255.255.255.0
ip default-gateway 10.103.1.1
no shutdown
```

