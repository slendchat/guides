Display kernel routing table
```
netstat -rn
```
result:
```
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         10.122.60.1     0.0.0.0         UG        0 0          0 ens33
10.122.60.0     0.0.0.0         255.255.255.0   U         0 0          0 ens33
```

display network interface statistics
```
netstat -i
```
result:
Kernel Interface table
Iface             MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
ens33            1500 13501775      0    406 0      17849242      0      0      0 BMRU
lo              65536 103173029      0      0 0      103173029      0      0      0 LRU

- The `-OK` suffixed fields indicate successfully received (RX) or transferred (TX) packets.
- The `-ERR` suffixed fields indicate connections with errors.
- The `-DRP` suffixed fields indicate the amount of packets dropped.
- The `-OVR` suffixed fields indicate the amount of packets lost due to overrun.

