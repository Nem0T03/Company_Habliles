```markdown
# 1. Cấu Hình EtherChannel

Trên Router R5 và R6:

### Cấu hình EtherChannel trên R5

```bash
en
conf t
int range e1/0-1
switchport trunk encapsulation dot1q
switchport mode trunk
channel-group 1 mode on
exit
int port-channel 1
ip add 192.168.10.1 255.255.255.0
no shut
end
show etherchannel summary
```

### Cấu hình EtherChannel trên R6

```bash
en
conf t
int range e1/0-1
switchport trunk encapsulation dot1q
switchport mode trunk
channel-group 1 mode on
exit
int port-channel 1
ip add 192.168.10.1 255.255.255.0
no shut
end
show etherchannel summary
```

# 2. Cấu Hình VTP (VLAN Trunking Protocol)

Trên Switch R1 và R2:

### Cấu hình VTP trên Switch R1

```bash
en
conf t
vtp domain abc.com
vtp mode server
vtp password 123
vlan 10
vlan 20
end
show vtp status
show vlan
```

### Cấu hình VTP trên Switch R2

```bash
en
conf t
vtp domain abc.com
vtp mode server
vtp password 123
vlan 30
vlan 40
end
show vtp status
show vlan
```

# 3. Gán Port cho các VLAN

Trên Switch R7 và R8:

### Gán Port cho VLAN trên Switch R7

```bash
en
conf t
int e0/2
switchport mode access
switchport access vlan 10
exit
int e0/3
switchport mode access
switchport access vlan 20
end
show vlan
```

### Gán Port cho VLAN trên Switch R8

```bash
en
conf t
int e0/2
switchport mode access
switchport access vlan 30
exit
int e0/3
switchport mode access
switchport access vlan 40
end
show vlan
```

# 4. Cấu Hình SVI VLAN và HSRP

Trên Multilayer Switch R5 và R6:

### Cấu hình SVI và HSRP trên Multilayer Switch R5

```bash
en
conf t
ip routing
int vlan 10
ip add 172.16.10.1 255.255.255.0
no shut
standby 1 ip 172.16.10.3
standby 1 priority 20
standby 1 preempt
exit
int vlan 20
ip add 172.16.20.1 255.255.255.0
no shut
standby 2 ip 172.16.20.3
standby 2 priority 20
standby 2 preempt
exit
show standby brief
```

### Cấu hình SVI và HSRP trên Multilayer Switch R6

```bash
en
conf t
ip routing
int vlan 30
ip add 172.16.30.2 255.255.255.0
no shut
standby 3 ip 172.16.30.3
standby 3 priority 20
standby 3 preempt
exit
int vlan 40
ip add 172.16.40.2 255.255.255.0
no shut
standby 4 ip 172.16.40.3
standby 4 priority 20
standby 4 preempt
exit
show standby brief
```

# 5. Cấu Hình DHCP trên Multilayer Switch

Trên Multilayer Switch R5 và R6:

### Cấu hình DHCP trên Multilayer Switch R5

```bash
en
conf t
ip dhcp pool Vlan1
network 172.16.10.0 255.255.255.0
default-router 172.16.10.3
dns-server 8.8.8.8
exit
ip dhcp pool Vlan2
network 172.16.20.0 255.255.255.0
default-router 172.16.20.3
dns-server 8.8.8.8
exit
```

### Cấu hình DHCP trên Multilayer Switch R6

```bash
en
conf t
ip dhcp pool Vlan3
network 172.16.30.0 255.255.255.0
default-router 172.16.30.3
dns-server 8.8.8.8
exit
ip dhcp pool Vlan4
network 172.16.40.0 255.255.255.0
default-router 172.16.40.3
dns-server 8.8.8.8
exit
```

# 6. Cấu Hình Firewall

Trên Firewall 1 và Firewall 2:

### Cấu hình Firewall 1

```bash
config system interface
edit port3
set mode static
set ip 192.168.109.10 255.255.255.0
set allowaccess http https ping telnet ssh
end
exe ping 192.168.109.2
show system interface
```

### Cấu hình Firewall 2

```bash
config system interface
edit port3
set mode static
set ip 192.168.109.11 255.255.255.0
set allowaccess http https ping telnet ssh
end
exe ping 192.168.109.2
show system interface
```

# 7. Cấu Hình Router Layer 3 và Kết Nối với Firewall

Trên Switch Layer 3 (R5 và R6):

### Cấu hình Switch Layer 3 trên R5

```bash
en
conf t
vlan 200
int vlan 200
ip add 192.168.200.1 255.255.255.0
no shut
exit
ip route 0.0.0.0 0.0.0.0 192.168.200.2
int range e0/0, e1/0
switchport mode access
switchport access vlan 200
end
show ip int brief
```

### Cấu hình Switch Layer 3 trên R6

```bash
en
conf t
vlan 210
int vlan 210
ip add 192.168.210.1 255.255.255.0
no shut
exit
ip route 0.0.0.0 0.0.0.0 192.168.210.2
int range e1/0, e0/0
switchport mode access
switchport access vlan 210
end
show ip int brief
show vlan
```

# 8. Cấu Hình DHCP Snooping

```bash
ip dhcp snooping
ip dhcp snooping vlan 2
int range e0/2-3
ip dhcp snooping trust
ip dhcp snooping database flash:snooping-db
show ip dhcp snooping
show ip dhcp snooping binding
```
```


