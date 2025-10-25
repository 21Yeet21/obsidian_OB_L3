enable
configure terminal
hostname L10-R2

interface Loopback0
 ip address 10.10.2.2 255.255.255.255

interface Fa0/0
 description Vers L10-R4
 ip address 10.10.24.2 255.255.255.0
 no shutdown

interface Fa0/1
 description Vers L10-R1
 ip address 10.10.12.2 255.255.255.0
 no shutdown

interface Fa1/0
 description Vers L10-R3
 ip address 10.10.23.2 255.255.255.0
 no shutdown

router ospf 10
 network 10.0.0.0 0.255.255.255 area 0

ip cef
end
write memory
