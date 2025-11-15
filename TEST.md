1️⃣ Router 7206VXR
conf t
int fa0/0
 ip address 192.168.1.1 255.255.255.252   ! to S1
 no shut
!
int fa1/0
 ip address dhcp                         ! fake Internet
 no shut
!
ip route 10.10.0.0 255.255.255.0 192.168.1.2
 #ip route 10.20.0.0 255.255.255.0 192.168.1.2
end
wr


---


2️⃣ Switch11 (L3 A = S1) — PBR applied here


conf t
ip routing

!── LAN VLAN
vlan 10
 name LAN-LEFT
int vlan10
 ip address 10.10.0.1 255.255.255.0
 no shut

!── Access link to R15
int gi0/2
 switchport mode access
 switchport access vlan 10
 no shut

!── OUT VLAN
vlan 50
 name TO-FW-OUT
int vlan50
 ip address 10.50.0.1 255.255.255.252
 no shut

!── IN VLAN
vlan 100
 name FROM-FW-IN
int vlan100
 ip address 10.100.0.1 255.255.255.252
 no shut

!── Trunk to S2
int gi0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 50,100
 no shut

!── Link to Router
int gi0/0
 no switchport
 ip address 192.168.1.2 255.255.255.252
 no shut

!──── Policy-Based Routing
ip access-list extended LAN-TO-INTERNET
 permit ip 10.10.0.0 0.0.0.255 any

route-map SEND_TO_FW permit 10
 match ip address LAN-TO-INTERNET
 set ip next-hop 10.50.0.2          ! S2 → firewall path

interface vlan10
 ip policy route-map SEND_TO_FW     ! apply PBR to LAN traffic

!──── Static routes (normal routing table)
ip route 0.0.0.0 0.0.0.0 192.168.1.1     ! default → router
ip route 10.50.0.0 255.255.255.252 10.50.0.2
ip route 10.100.0.0 255.255.255.252 10.100.0.2
end
wr



3️⃣ Switch12 (L3 B = S2)


conf t
ip routing

vlan 50
 name TO-FW-OUT
int vlan50
 ip address 10.50.0.2 255.255.255.252
 no shut

vlan 100
 name FROM-FW-IN
int vlan100
 ip address 10.100.0.2 255.255.255.252
 no shut

!── Trunk to S1 and FW
int gi0/0
 switchport mode trunk
 switchport trunk allowed vlan 50,100
 no shut
int gi0/1
 switchport mode trunk
 switchport trunk allowed vlan 50,100
 no shut

!── LAN on right side
vlan 20
 name LAN-RIGHT
int vlan20
 ip address 10.20.0.1 255.255.255.0
 no shut
int gi0/2
 switchport mode access
 switchport access vlan 20
 no shut

!── Static routes
ip route 10.10.0.0 255.255.255.0 10.50.0.1
ip route 0.0.0.0 0.0.0.0 10.100.0.3
end
wr





Routing (FortiOS CLI style):


config system interface
    edit "port1.50"
        set vdom "root"
        set interface "port1"
        set vlanid 50
        set ip 10.50.0.3 255.255.255.252
        set allowaccess ping
        set alias "inside-fw"
    next
    edit "port1.100"
        set vdom "root"
        set interface "port1"
        set vlanid 100
        set ip 10.100.0.3 255.255.255.252
        set allowaccess ping
        set alias "outside-fw"
    next
end



config router static
    edit 1
        set dst 0.0.0.0/0
        set gateway 10.100.0.1
        set device "port1.100"
    next
    edit 2
        set dst 10.10.0.0/24
        set gateway 10.50.0.2
        set device "port1.50"
    next
end












config router static
    
    edit 1
        set dst 0.0.0.0/0
        set device "port1.60"
         set gateway 10.60.0.1
    next
    edit 2
        set dst 10.10.0.0/24
        set gateway 10.60.0.1
        set device "port1.60"
    next
end


