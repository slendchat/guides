Display kernel routing table
```
netstat -rn
```
result:
```
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.109.2   0.0.0.0         UG        0 0          0 ens33
192.168.109.0   0.0.0.0         255.255.255.0   U         0 0          0 ens33
192.168.109.2   0.0.0.0         255.255.255.255 UH        0 0          0 ens33
```

display network interface statistics
```
netstat -i
```
result:
Kernel Interface table
Iface             MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
ens33            1500      334      0      0 0           325      0      0      0 BMRU
lo              65536       26      0      0 0            26      0      0      0 LRU

- The `-OK` suffixed fields indicate successfully received (RX) or transferred (TX) packets.
- The `-ERR` suffixed fields indicate connections with errors.
- The `-DRP` suffixed fields indicate the amount of packets dropped.
- The `-OVR` suffixed fields indicate the amount of packets lost due to overrun.

netstat
- `-t` for active TCP socket connections
- `-u` for active UDP socket connections
- `-w` for active RAW socket connections
- `-x` for active Unix socket connections
- `-a` option will display sockets that are listening for connection.

This command displays anything listening for incoming traffic and the port it is listening on.
```
sudo netstat -untlp
```

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      646/systemd-resolve
tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN      646/systemd-resolve
tcp6       0      0 :::22                   :::*                    LISTEN      1/init
udp        0      0 127.0.0.54:53           0.0.0.0:*                           646/systemd-resolve
udp        0      0 127.0.0.53:53           0.0.0.0:*                           646/systemd-resolve
udp        0      0 192.168.109.143:68      0.0.0.0:*                           638/systemd-network

|Header|Description|
|---|---|
|Proto|The connection protocol (TCP or UDP)|
|Recv-Q|Queue of bytes received or ready to be received|
|Send-Q|Queue of bytes ready to be sent|
|Local address|The details of the address and the local connection port (an asterisk indicates that the port is open)|
|Foreign address|The details of the address and the remote connection port (an asterisk indicates that the port is not yet established)|
|State|The state of the socket showing whether the connection to the port is established or not, and if it’s an open or a closed port|

Listing all active listening ports
```
netstat -l
```


list the ports that are being listened to. This works for root users on a Linux machine
```
sudo netstat -plnt
```





glossary
https://www.site24x7.com/learn/linux/netstat-command.html