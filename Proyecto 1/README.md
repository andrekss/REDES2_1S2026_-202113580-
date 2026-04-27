# REDES2_1S2026_-202113580-


## Subnetting VLANs (VLSM)

| VLAN        | Hosts | Red              | Máscara         | Primer Host   | Último Host   | Broadcast     |
| ----------- | ----- | ---------------- | --------------- | ------------- | ------------- | ------------- |
| Naranja IZQ | 6     | 192.188.80.0/28  | 255.255.255.240 | 192.188.80.1  | 192.188.80.14 | 192.188.80.15 |
| Verde IZQ   | 6     | 192.188.80.16/28 | 255.255.255.240 | 192.188.80.17 | 192.188.80.30 | 192.188.80.31 |
| Naranja DER | 6     | 192.188.80.32/29 | 255.255.255.248 | 192.188.80.33 | 192.188.80.38 | 192.188.80.39 |
| Verde DER   | 6     | 192.188.80.40/29 | 255.255.255.248 | 192.188.80.41 | 192.188.80.46 | 192.188.80.47 |
| ADMIN       | 6     | 192.188.80.48/29 | 255.255.255.248 | 192.188.80.49 | 192.188.80.54 | 192.188.80.55 |


## Subnetting enlaces (FLSM /30)

| Enlace  | Red           |
| ------- | ------------- |
| MS1-MS7 | 10.4.80.0/30  |
| MS1-MS2 | 10.4.80.4/30  |
| MS7-MS6 | 10.4.80.8/30  |
| MS2-MS6 | 10.4.80.12/30 |
| MS7-MS9 | 10.4.80.16/30 |
| MS7-MS8 | 10.4.80.20/30 |
| MS2-MS3 | 10.4.80.24/30 |
| MS3-MS4 | 10.4.80.28/30 |
| MS4-MS5 | 10.4.80.32/30 |

## VLAN

| VLAN                               | ID |
| ---------------------------------- | -- |
| VLAN_Naranja_EdificioIZQ_202113580 | 10 |
| VLAN_Verde_EdificioIZQ_202113580   | 20 |
| VLAN_Naranja_EdificioDER_202113580 | 30 |
| VLAN_Verde_EdificioDER_202113580   | 40 |
| VLAN_ADMIN_202113580               | 99 |

## VTP

### Dominio

chapinred

### Password

cisco

## MS1

bash
```
enable
conf t
hostname MS1

! VTP
vtp mode server
vtp domain chapinred
vtp password cisco

! VLAN
vlan 10
name VLAN_Naranja_EdificioIZQ_202113580
vlan 20
name VLAN_Verde_EdificioIZQ_202113580
vlan 30
name VLAN_Naranja_EdificioDER_202113580
vlan 40
name VLAN_Verde_EdificioDER_202113580
vlan 99
name VLAN_ADMIN_202113580

ip routing

! hacia DHCP1
interface gi1/0/1
description DHCP1
no switchport
ip address 10.4.80.1 255.255.255.252

! hacia DHCP2
interface gi1/0/2
description DHCP2
no switchport
ip address 10.4.80.5 255.255.255.252

! hacia MS7
interface gi1/0/3
description MS7
no switchport
ip address 10.4.80.9 255.255.255.252

! hacia MS2
interface gi1/0/4
description MS2
no switchport
ip address 10.4.80.13 255.255.255.252

router ospf 1
network 10.4.80.0 0.0.0.255 area 0
network 192.188.80.0 0.0.0.255 area 0
```