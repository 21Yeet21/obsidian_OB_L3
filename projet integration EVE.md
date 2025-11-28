
conf base

![[Pasted image 20251013180622.png]]


vlan connf 
![[Pasted image 20251013180809.png]]



vlan access

![[Pasted image 20251013181230.png]]




trunk vlan 
![[Pasted image 20251013182712.png]]



L3 conf 

vlan declaration

![[Pasted image 20251013183157.png]]


trunk


![[Pasted image 20251013183944.png]]


enable routing 

![[Pasted image 20251013184334.png]]


vlan ips 

![[Pasted image 20251013185126.png]]

![[Pasted image 20251013190654.png]]









![[Pasted image 20251013193738.png]]



![[Pasted image 20251025113325.png]]

![[Pasted image 20251025113338.png]]





![[Pasted image 20251025120259.png]]






![[Pasted image 20251109223459.png]]


session 5

ping vlan 30 too fw 


![[Pasted image 20251102231855.png]]

![[Pasted image 20251102231833.png]]


![[Pasted image 20251104121212.png]]


![[Pasted image 20251104121053.png]]




![[Pasted image 20251111182327.png]]

![[Pasted image 20251111185104.png]]



---

## 🧱 **Mini Topology Summary**

### 🔹 Devices & Networks

|Device|VLAN|IP Address|Role|
|---|---|---|---|
|**Firewall**|VLAN 200|192.168.200.2/24|Link to L3 switch|
|**Firewall**|VLAN 10|192.168.10.254/24|DHCP Server for users|
|**L3 Switch (SVI)**|VLAN 200|192.168.200.1/24|Route to firewall|
|**L3 Switch (SVI)**|VLAN 10|192.168.10.1/24|Gateway for users|
|**PC (Client)**|VLAN 10|DHCP → 192.168.10.x|User device|

---

## ⚙️ **Traffic Flow**

1. **PC in VLAN 10** sends a DHCP Discover broadcast.
    
2. The **L3 switch (VLAN10 SVI)** receives it and forwards it:
    
    - Either directly to firewall VLAN10 interface (if both share VLAN 10 trunk)
        
    - Or through **DHCP relay (`ip helper-address`)** to VLAN 200 if using routed design.
        
3. **Firewall DHCP server** responds with an offer from `192.168.10.254`.
    
4. The **switch passes** the reply back to the PC in VLAN 10.
    
5. The PC receives:
    
    - IP address (e.g., 192.168.10.50)
        
    - Gateway = 192.168.10.1 (switch)
        
    - DNS = firewall or external
        
6. Switch routes all VLAN 10 traffic → VLAN 200 → firewall → Internet.
    

---

## 🔁 **Key Configurations Recap**

### 🔸 On Switch

```bash
vlan 10
vlan 200

interface vlan 10
 ip helper-address 192.168.200.2
 no shut

interface vlan 200
 ip address 192.168.200.1 255.255.255.0
 no shut

interface Gi0/1   # (firewall link)
 switchport mode trunk
 switchport trunk allowed vlan 10,200
 
 interface Gi0/2   
 switchport mode access
 switchport access vlan 10


ip route 0.0.0.0 0.0.0.0 192.168.200.2
```

### 🔸 On Firewall

- VLAN 200: `192.168.200.2/24`
    
- VLAN 10: `192.168.10.254/24`
    
- DHCP server on VLAN 10:
    
    ```
    Network: 192.168.10.0/24
    Range: 192.168.10.50 – 192.168.10.100
    Gateway: 192.168.10.1
    DNS: 192.168.10.254 or external
    ```
    
- Static route to VLAN 10 (if not directly connected):
    
    ```
    192.168.10.0/24 via 192.168.200.1
    ```
    

---

## ✅ **Result**

- PCs in VLAN 10 automatically receive IPs from the **firewall DHCP server**.
    
- The **L3 switch routes** between VLANs internally.
    
- The **firewall handles** DHCP, NAT, and Internet access.
    
- All VLANs are trunked properly and Layer 3 routing + DHCP relay work together.
    

---

Would you like me to make a **diagram image** of this topology (with IPs and VLANs labeled) so you can keep it for reference or documentation?















Great — two clean choices that meet your goal **(VLAN 10 must NOT be routed by the switch; other VLANs must not see VLAN 10)**. I’ll give both options (simple and QinQ), with exact config snippets and notes so you can pick and apply immediately.

---

# Option A — Recommended: Pure L2 trunk (firewall is gateway)

Keep the switch purely Layer-2 for VLAN 10. The switch does **NOT** have an SVI for VLAN 10 and does **not** route it. The trunk to the firewall carries VLAN 10 tagged. Firewall does all routing, DHCP and inter-VLAN isolation.

Why choose this

- Simple, robust, supported everywhere.
    
- Other VLANs on the switch will not reach VLAN 10 unless you explicitly trunk them to the firewall and create firewall rules.
    
- No DHCP relay needed.
    

Switch (Cisco IOS) — firewall on Gi0/1:

```bash
! create VLAN
vlan 10
 name VLAN_USERS

! access ports for clients
interface GigabitEthernet0/2
 switchport mode access
 switchport access vlan 10
 no shutdown

! trunk to firewall
interface GigabitEthernet0/1
 switchport trunk encapsulation dot1q   ! only on older IOS that require it
 switchport mode trunk
 switchport trunk allowed vlan 10,other-vlans-you-want
 no shutdown

! IMPORTANT: do NOT create "interface Vlan10" on the switch
```

Firewall:

- Configure parent physical as trunk carrying VLAN 10.
    
- Create subinterface / VLAN10 interface with IP `192.168.10.1` (firewall as gateway).
    
- Enable DHCP on VLAN10: pool `192.168.10.50-100`, gateway `192.168.10.1`.
    
- Add firewall rules to control which other VLANs can reach VLAN10 (deny by default).
    

Result: Clients in VLAN10 get IPs directly from firewall; switch never routes VLAN10.

---

# Option B — If you _must_ encapsulate VLAN 10 inside VLAN 200 on the transit link (QinQ / double-tag)

Use this if you require that **all traffic between switch and firewall be carried on outer VLAN 200** for monitoring, separation, or because your upstream only accepts VLAN200. This uses 802.1ad (QinQ): outer tag = VLAN200, inner tag = VLAN10. The switch keeps VLAN10 as L2 and does not route it.

Important prerequisites

- Your switch and firewall must support QinQ (802.1ad). Not all home/consumer devices do.
    
- Firewall must be able to decapsulate QinQ or be configured to receive outer tag and inner VLANs.
    

High-level idea

- Access ports for clients: normal access VLAN 10.
    
- On the switch edge that goes to the firewall, configure dot1q-tunnel (QinQ) so frames get an extra outer tag 200.
    
- Firewall receives frames with outer tag 200 and inner 10 — it can then handle VLAN10 as usual.
    

Example (Cisco IOS x.x — classic dot1q-tunnel):

```bash
! client access ports
interface GigabitEthernet0/2
 switchport mode access
 switchport access vlan 10
 no shutdown

! provider-facing port -> QinQ
interface GigabitEthernet0/1
 switchport trunk encapsulation dot1q
 switchport mode dot1q-tunnel
 switchport access vlan 10       ! inner VLAN to be tunneled
 switchport trunk native vlan 200 ! outer/native tag 200 (behavior depends on IOS)
 no shutdown
```

On the firewall side you must configure it to accept VLAN200 as outer and extract inner VLAN 10. Implementation on firewall varies:

- Some firewall OSes (or switches) support “QinQ termination” / configure outer VLAN 200 interface and allow inner VLANs.
    
- Alternatively, configure the firewall to accept VLAN 200 as trunk and within it create a subinterface for inner VLAN 10 if your firewall supports QinQ termination.
    

Notes & caveats

- QinQ syntax and features differ between platforms. Newer Catalyst platforms use service-instances; some firewalls (pfSense out of the box) do not do QinQ termination without extra packages or special NIC handling.
    
- If your firewall cannot do QinQ, don’t use this option.
    

---

# Which to choose?

- If your aim is simply that the **switch must not route VLAN 10** and **other VLANs must not see VLAN 10**, pick **Option A (L2 trunk)**. It’s simple and works everywhere.
    
- If you have a strong requirement that _everything on the wire to the firewall be tagged with VLAN 200_ (outer tag) for transit/monitoring, **Option B (QinQ)** is the way — only if both devices support it.
    

---

# Quick checklist to assure isolation (for Option A)

-  Remove any `interface Vlan10` SVI on the switch.
    
-  Trunk port to firewall includes VLAN 10.
    
-  Firewall has VLAN10 subinterface (IP and DHCP).
    
-  No `ip helper-address` on switch (not needed).
    
-  Firewall rules deny access from other VLANs to VLAN10 unless explicitly allowed.
    
-  Test: client gets DHCP and cannot ping hosts in other VLANs.
    

---

Tell me which option you want to apply (A or B) and which firewall you use (pfSense, FortiGate, Cisco ASA, etc.). I’ll give **exact device-specific commands** (pfSense web clicks or FortiGate/Cisco examples) ready to paste.

TRUNK VLAN 10,200
![[Pasted image 20251112230122.png]]

TRUNK VLAN 200
![[Pasted image 20251112230312.png]]



![[Pasted image 20251113211958.png]]


![[Pasted image 20251113212111.png]]


![[Pasted image 20251113212137.png]]

![[Pasted image 20251113212207.png]]

interconnexion entre vlan 300 et 301

![[Pasted image 20251123135350.png]]


![[Pasted image 20251123135414.png]]

WAN FW
![[Pasted image 20251123135802.png]]

![[Pasted image 20251123135645.png]]

![[Pasted image 20251123135920.png]]



![[Pasted image 20251123140429.png]]





![[Pasted image 20251123141912.png]]
![[Pasted image 20251123141940.png]]

![[Pasted image 20251123142004.png]]

du routeur vers vlan 100
![[Pasted image 20251123142112.png]]

![[Pasted image 20251123142503.png]]





![[Pasted image 20251123153945.png]]



![[Pasted image 20251123154542.png]]


crypto isakmp policy 10
 encryption des
 hash sha256
 authentication pre-share
 group 2
 lifetime 28800
!
crypto isakmp key Eve123 address 10.10.10.2


ip access-list extended VPN-TRAFFIC
 permit ip 192.168.30.0 0.0.0.255 172.16.0.64 0.0.0.63
 permit ip 192.168.30.0 0.0.0.255 172.16.0.192 0.0.0.63



show crypto ipsec sa

![[Pasted image 20251123170130.png]]


![[Pasted image 20251123170202.png]]


![[Pasted image 20251123170228.png]]

