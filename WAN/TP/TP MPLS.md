
---

# 🧠 **MPLS Complete Summary (Chapters 1–5)**

---

## 🔹 **1 – Introduction to MPLS**

### 🧩 Concept

- **MPLS (Multiprotocol Label Switching)** routes packets based on **labels**, not IP headers.
    
- Labels sit **between Layer 2 and 3**, enabling _Label Swapping_ (fast switching).
    
- Originally designed for speed; now used for **VPNs** and **Traffic Engineering (TE)**.
    

### ⚙️ Key Features

|Feature|Description|
|---|---|
|**Ingress LSR**|Adds label (entry into MPLS cloud)|
|**Egress LSR**|Removes label (exit point)|
|**P Router (LSR)**|Performs label switching only|
|**PE Router**|Connects customers (CEs) to MPLS backbone|

---

## 🔹 **2 – Lab Setup (Pods L10 & L20)**

### Devices

|Router|Model|Function|
|---|---|---|
|R1, R4, R5|3620|Core / PE|
|R2, R3|3640|Core / P|
|R6, R7|2600|CE|

- IOS 12.2(0.4)
    
- IGP = **OSPF**
    

### Address Convention

- Loopback0 : `10.10.x.x`
    
- Link Rx–Ry : `10.10.xy.0/24`
    
- IP Rx : `10.10.xy.x`, Ry : `10.10.xy.y`
    

---

## 🔹 **3 – Core MPLS Principles**

### ⚙️ Enable MPLS on Routers

```bash
conf t
ip cef
interface s0/0
 tag-switching ip
no shut
```

> `ip cef` is **mandatory** (MPLS uses TFIB via CEF).

---

### 🧱 **Label Distribution Protocols**

|Protocol|Purpose|Command|
|---|---|---|
|**TDP / LDP**|Label exchange for IGP routes|`tag-switching ip` or `mpls ip`|
|**RSVP-TE**|Label assignment for TE LSPs|auto with TE tunnels|
|**MP-BGP**|Label exchange for VPNv4 routes|inside `address-family vpnv4`|

Check neighbors :

```bash
show tag-switching tdp neighbor
show tag-switching tdp discovery
```

---

### 🧭 **Label Tables**

|Table|Meaning|Command|
|---|---|---|
|**TIB** (Tag Information Base)|Stores learned labels|`show tag tdp bindings`|
|**TFIB** (Tag Forwarding Info Base)|Used for packet switching|`show tag-switching forwarding`|
|**CEF Table**|IP→Next-Hop+Label mapping|`show ip cef <prefix>`|

Example :

```bash
Local tag: 24 → Outgoing tag: 21 via Se0/1
```

---

### 🧩 **Penultimate Hop Popping (PHP)**

- The penultimate router removes the top label (`implicit-null`) before sending to egress.  
    Check:
    

```bash
show tag-switching forwarding | include Pop
```

---

### ⚡ **Label Retention Modes**

|Mode|Use Case|
|---|---|
|**Liberal**|Frame mode interfaces – faster convergence|
|**Conservative**|ATM interfaces – label on demand|

---

### 💡 **MPLS over ATM**

- Uses **downstream on demand** label distribution.
    
- Label = VPI/VCI mapping; optional VC Merge to limit labels.
    

---

### 🔗 **Label Stacking**

- Multiple labels → used in **VPNs** and **TE**.  
    Only the top label is processed per hop.
    

---

### 📦 **MPLS Header Format**

|Field|Bits|Function|
|---|---|---|
|Label|20|Label ID|
|Exp|3|QoS bits|
|S|1|Bottom of stack indicator|
|TTL|8|Time To Live|

---

### ⚙️ **IGP for MPLS**

Use a link-state protocol (OSPF / IS-IS):

```bash
router ospf 10
 network 10.0.0.0 0.255.255.255 area 0
```

---

## 🔹 **4 – MPLS VPN (Provider Edge Services)**

### 🧩 **Concept**

- Each customer (VPN) has its own **VRF (Virtual Routing and Forwarding)**.
    
- VPN routes are advertised between PEs using **MP-BGP**.
    
- **RD (Route Distinguisher)** → makes prefix unique.
    
- **RT (Route Target)** → controls which VRF imports/exports routes.
    

---

### ⚙️ **PE Configuration Example**

```bash
ip vrf RED
 rd 100:2
 route-target export 500:1000
 route-target import 500:1000
!
interface Fa0/0
 ip vrf forwarding RED
 ip address 100.10.57.5 255.255.255.0
!
router bgp 10
 address-family ipv4 vrf RED
  redistribute connected
  neighbor 100.10.57.7 remote-as 102
  neighbor 100.10.57.7 activate
 exit-address-family
!
address-family vpnv4
 neighbor 10.10.1.1 activate
 neighbor 10.10.1.1 send-community extended
 exit-address-family
```

---

### 🧱 **CE Router Example (BGP)**

```bash
router bgp 102
 network 100.10.7.7 mask 255.255.255.255
 neighbor 100.10.57.5 remote-as 10
```

Or with **RIP**:

```bash
router rip
 version 2
 network 100.0.0.0
 no auto-summary
```

---

### 🔍 **Verification**

```bash
show ip vrf
show ip bgp vpnv4 all
show ip bgp vpnv4 vrf <name>
show ip bgp vpnv4 vrf <name> tags
```

---

### 🧠 **Label Stacking in VPNs**

- 2 labels are used :
    
    1. **Outer Label** – transit label between PEs
        
    2. **Inner Label** – VPN label → selects VRF at destination
        

---

### 🌐 **Internet Access Models**

|Method|Description|
|---|---|
|**Static Default Route**|Simple route per VRF (`ip route vrf GREEN 0.0.0.0 ...`)|
|**Dynamic Default Route (Hub-Spoke)**|Shared default RT (500:1001) from central PE|
|**Optimum Routing**|Each PE has global Internet routes (BGP iBGP)|

---

### 🌍 **Inter-AS (Inter-domain MPLS/VPN)**

- Uses **MP-eBGP** between AS’s.
    
- Disable LDP/TDP on inter-AS link:
    
    ```bash
    no tag-switching ip
    neighbor x.x.x.x next-hop-self
    ```
    
- Exchanged VPNv4 routes carry a single label (inter-AS label).
    

---

## 🔹 **5 – Traffic Engineering (TE)**

### 🎯 **Goal**

Use MPLS tunnels (LSPs) to manually or dynamically steer traffic along non-IGP paths for load-balancing and resilience.

---

### 🧭 **Enable Traffic Engineering**

```bash
mpls traffic-eng tunnels
```

---

### 🧩 **IGP Configuration**

#### OSPF Example :

```bash
router ospf 10
 network 10.0.0.0 0.255.255.255 area 0
 mpls traffic-eng router-id Loopback0
 mpls traffic-eng area 0
```

#### IS-IS Example :

```bash
router isis
 net 49.0020.4444.4444.4444.00
 metric-style wide
 mpls traffic-eng router-id Loopback0
 mpls traffic-eng level-1
```

---

### 🔧 **Interface Configuration for TE**

```bash
interface s0/0
 ip address 10.20.24.4 255.255.255.0
 tag-switching ip
 mpls traffic-eng tunnels
 ip rsvp bandwidth 100 100
```

> RSVP reserves bandwidth for tunnels;  
> `mpls traffic-eng tunnels` allows LSPs to pass.

---

### 🧠 **Tunnels (Explicit vs Dynamic)**

#### Explicit Tunnel Example

```bash
interface Tunnel1
 ip unnumbered Loopback0
 tunnel destination 10.20.3.3
 tunnel mode mpls traffic-eng
 tunnel mpls traffic-eng autoroute announce
 tunnel mpls traffic-eng bandwidth 10
 tunnel mpls traffic-eng path-option 1 explicit name WAY1
!
ip explicit-path name WAY1 enable
 next-address 10.20.24.2
 next-address 10.20.12.1
 next-address 10.20.13.3
```

#### Dynamic Tunnel Example

```bash
interface Tunnel2
 ip unnumbered Loopback0
 tunnel destination 10.20.3.3
 tunnel mode mpls traffic-eng
 tunnel mpls traffic-eng autoroute announce
 tunnel mpls traffic-eng bandwidth 10
 tunnel mpls traffic-eng affinity 0x10 mask 0x11
 tunnel mpls traffic-eng path-option 1 dynamic
```

---

### ⚙️ **Verification**

```bash
show mpls traffic-eng tunnels
show ip rsvp interface
show ip rsvp neighbor
show ip cef <dest>
```

---

### 🔁 **Re-optimization**

- The router can **rebuild a better tunnel path** dynamically without service interruption.
    
- Old tunnel removed after new one is active.
    

---

### 🔗 **TE with MPLS/VPN**

- Two tunnels (LSPs) must exist (one per direction).
    
- Use `tag-switching ip` on tunnel interfaces.
    
- Label stack = **[TE label] + [PE label] + [VPN label]**.
    

---

## 🧾 **Quick Command Cheat-Sheet**

|Category|Key Commands|
|---|---|
|**CEF Activation**|`ip cef`|
|**Enable MPLS**|`tag-switching ip` or `mpls ip`|
|**Check Neighbors**|`show tag-switching tdp neighbor`|
|**View Bindings**|`show tag tdp bindings`|
|**Forwarding Table**|`show tag-switching forwarding`|
|**CEF Lookup**|`show ip cef <prefix>`|
|**View VRF Table**|`show ip vrf`|
|**View VPNv4 Routes**|`show ip bgp vpnv4 all`|
|**RSVP/TE Status**|`show mpls traffic-eng tunnels`, `show ip rsvp interface`|
|**Traceroute Labels**|`traceroute <ip>` or `traceroute vrf <vrf> <ip>`|

---

## 🧩 **Key Takeaways**

|Topic|Core Idea|
|---|---|
|**MPLS Basics**|Fast packet forwarding using labels instead of routing tables|
|**VPN MPLS**|Multi-tenant routing with VRFs + MP-BGP (label stack = PE + VPN)|
|**Traffic Engineering**|Controlled path selection based on bandwidth + affinity|
|**PHP**|Penultimate router removes top label for efficiency|
|**Label Retention**|Liberal = fast convergence; Conservative = less memory|
|**Verification Tools**|`show ip cef`, `show tag-switching`, `show ip bgp vpnv4`|

---

✅ **This summary = all you need to configure, verify, and explain MPLS / MPLS-VPN / TE from scratch.**

Would you like me to turn this into a **formatted PDF “MPLS Command & Concept Guide”** (clean layout + quick index) for offline reference?