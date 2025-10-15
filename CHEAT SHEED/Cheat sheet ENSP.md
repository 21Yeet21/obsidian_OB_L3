

| Order | Section            | Purpose                 |
| ----- | ------------------ | ----------------------- |
| 1     | VLANs + Trunking   | Layer 2 segmentation    |
| 2     | STP / RSTP / MSTP  | Prevent loops           |
| 3     | LACP (Eth-Trunk)   | Link aggregation        |
| 4     | Inter-VLAN Routing | VLAN communication      |
| 5     | OSPF / RIP / BGP   | Dynamic routing         |
| 6     | VRRP               | Gateway redundancy      |
| 7     | DHCP               | IP assignment           |
| 8     | ACL                | Security filtering      |
| 9     | NAT                | Internet access         |
| 10    | Optional           | Monitoring / QoS / QinQ |
## 🧩 VLANs + Trunking (Huawei eNSP)

### 🎯 Purpose

- VLANs segment Layer 2 networks into isolated broadcast domains.
    
- Trunk links allow multiple VLANs to cross a single physical interface between switches.
    

---

### ⚙️ VLAN Configuration (Access ports)

```bash
<Huawei> system-view
[Huawei] vlan 10                     # create VLAN 10
[Huawei-vlan10] quit

[Huawei] interface GigabitEthernet0/0/1
[Huawei-GigabitEthernet0/0/1] port link-type access
[Huawei-GigabitEthernet0/0/1] port default vlan 10
[Huawei-GigabitEthernet0/0/1] quit
```

> ✅ **Tip:** “access” ports carry only one VLAN (untagged).

---

### 🌉 Trunk Configuration (Tagged ports)

```bash
[Huawei] interface GigabitEthernet0/0/2
[Huawei-GigabitEthernet0/0/2] port link-type trunk
[Huawei-GigabitEthernet0/0/2] port trunk allow-pass vlan 10 20 30
[Huawei-GigabitEthernet0/0/2] quit
```

> ✅ “trunk” allows multiple VLANs, typically used between switches or switch–router connections.

---

### 🔀 Hybrid Mode (Access + Trunk mix)

```bash
[Huawei] interface GigabitEthernet0/0/3
[Huawei-GigabitEthernet0/0/3] port link-type hybrid
[Huawei-GigabitEthernet0/0/3] port hybrid pvid vlan 10
[Huawei-GigabitEthernet0/0/3] port hybrid untagged vlan 10
[Huawei-GigabitEthernet0/0/3] port hybrid tagged vlan 20 30
```

> ✅ Hybrid mode = mix of tagged and untagged VLANs (used for special cases, e.g., IP phones).

---

### 🧠 Inter-VLAN Communication (SVI / VLANIF)

```bash
[Huawei] interface Vlanif10
[Huawei-Vlanif10] ip address 192.168.10.1 255.255.255.0
[Huawei] interface Vlanif20
[Huawei-Vlanif20] ip address 192.168.20.1 255.255.255.0
```

> ✅ VLANIF interfaces = Layer 3 gateways for each VLAN (routed by switch or router).

---

### 🔍 Verification Commands

```bash
display vlan                           # list VLANs and member ports
display port vlan                      # show VLAN per port
display interface brief                # check interface status
display interface gigabitethernet 0/0/1
display interface trunk                # trunk info
display mac-address vlan 10            # MACs learned in VLAN 10
```

---

Perfect 👌 Let’s move to **STP / RSTP / MSTP** — one of the most important Layer 2 protocols right after VLANs and trunking.  
Here’s your **complete Huawei eNSP cheatsheet section**, including config, verification, and what else you must not forget.

---

## 🧩 STP / RSTP / MSTP (Spanning Tree Protocol Family)

### 🎯 Purpose
Prevents **Layer 2 loops** when multiple switches are interconnected through redundant links.  
It ensures only one active path per VLAN or per MST instance.

---

### ⚙️ Enable and Choose Mode
```bash
<Huawei> system-view
[Huawei] stp enable              # enable STP globally (if not enabled)
[Huawei] stp mode stp            # classic STP
[Huawei] stp mode rstp           # rapid version (faster)
[Huawei] stp mode mstp           # multiple spanning tree (per VLAN mapping)
```

> ✅ Only one mode is active at a time (STP, RSTP, or MSTP).

---

### 🌲 STP Basic Configuration (Legacy)
```bash
[Huawei] stp priority 0                     # make this switch the root bridge
[Huawei] interface GigabitEthernet0/0/1
[Huawei-GigabitEthernet0/0/1] stp cost 2000 # manually set path cost
[Huawei-GigabitEthernet0/0/1] stp edged-port enable  # portfast (edge port)
```

---

### ⚡ RSTP Configuration (Recommended in labs)
```bash
[Huawei] stp mode rstp
[Huawei] stp enable
[Huawei] stp priority 4096                  # lower value = more likely root
[Huawei] interface GigabitEthernet0/0/1
[Huawei-GigabitEthernet0/0/1] stp edged-port enable
```
> ✅ RSTP converges faster and supports auto-edge detection.

---

### 🌐 MSTP Configuration (For multiple VLAN instances)
```bash
[Huawei] stp mode mstp
[Huawei] stp enable

# Configure MST region
[Huawei] stp region-configuration
[Huawei-mst-region] region-name RG1
[Huawei-mst-region] revision-level 1
[Huawei-mst-region] instance 1 vlan 10 20
[Huawei-mst-region] instance 2 vlan 30
[Huawei-mst-region] active region-configuration
[Huawei-mst-region] quit

# Set priority per MST instance
[Huawei] stp instance 1 priority 4096
[Huawei] stp instance 2 priority 8192
```
> ✅ MSTP lets you have **different root switches** for different VLAN groups.

---

### 🧱 Port Configuration (All Modes)
```bash
[Huawei] interface GigabitEthernet0/0/2
[Huawei-GigabitEthernet0/0/2] stp enable
[Huawei-GigabitEthernet0/0/2] stp edged-port enable
[Huawei-GigabitEthernet0/0/2] stp cost 100
[Huawei-GigabitEthernet0/0/2] stp port-priority 64
```

---

### 🔍 Verification Commands
```bash
display stp                              # global STP info
display stp brief                        # summary of all interfaces
display stp interface GigabitEthernet0/0/1
display stp vlan 10                      # STP info per VLAN
display stp region-configuration         # MST region info
display stp instance brief               # MST instance overview
display stp process brief                # STP process state
```

---

### ⚠️ Protection Features (Optional but important)
```bash
[Huawei] interface GigabitEthernet0/0/1
[Huawei-GigabitEthernet0/0/1] stp bpdu-protection enable      # protects edge ports
[Huawei-GigabitEthernet0/0/1] stp root-protection enable      # prevents wrong root
[Huawei-GigabitEthernet0/0/1] stp loop-protection enable      # prevents loops
```

---

### 💾 Save Configuration
```bash
save
```

Perfect 👌 — here’s your **complete Huawei eNSP cheatsheet for LACP (Eth-Trunk)**.  
This section builds right after **VLAN + STP**, because LACP provides **redundancy and load balancing** for trunk links.

---

## 🧩 LACP (Eth-Trunk) – Link Aggregation Control Protocol

### 🎯 Purpose

LACP (IEEE 802.3ad) combines multiple physical interfaces into **one logical interface (Eth-Trunk)** for:

- Higher bandwidth
    
- Link redundancy
    
- Load balancing
    
- Better fault tolerance
    

---

### ⚙️ Create an Eth-Trunk (LACP Group)

```bash
<Huawei> system-view
[Huawei] interface Eth-Trunk 1
[Huawei-Eth-Trunk1] mode lacp                   # Enable LACP mode
[Huawei-Eth-Trunk1] port link-type trunk        # Trunk to carry VLANs
[Huawei-Eth-Trunk1] port trunk allow-pass vlan all
[Huawei-Eth-Trunk1] lacp priority 100           # Lower = higher priority (optional)
```

> ✅ Use **manual** mode if you don’t want LACP negotiation:  
> `[Huawei-Eth-Trunk1] mode manual load-balance`

---

### 🔗 Add Member Interfaces to the Eth-Trunk

```bash
[Huawei] interface GigabitEthernet0/0/1
[Huawei-GigabitEthernet0/0/1] eth-trunk 1
[Huawei-GigabitEthernet0/0/1] quit

[Huawei] interface GigabitEthernet0/0/2
[Huawei-GigabitEthernet0/0/2] eth-trunk 1
[Huawei-GigabitEthernet0/0/2] quit
```

> ✅ All member interfaces **must have identical** settings (speed, duplex, VLANs, trunk type, etc.)

---

### 🔁 Optional: Load Balancing Mode

```bash
[Huawei-Eth-Trunk1] load-balance src-dst-mac     # (Default) based on source & destination MAC
# or
[Huawei-Eth-Trunk1] load-balance src-dst-ip      # based on IP
```

---

### 🧱 VLAN Trunk Configuration on Eth-Trunk

```bash
[Huawei] interface Eth-Trunk 1
[Huawei-Eth-Trunk1] port link-type trunk
[Huawei-Eth-Trunk1] port trunk allow-pass vlan 10 20 30
```

> ✅ Configure this just like a normal trunk port — Eth-Trunk behaves as a single logical trunk.

---

### 🔍 Verification Commands

```bash
display eth-trunk 1                  # Detailed information about Eth-Trunk 1
display eth-trunk summary            # Summary of all trunks
display link-aggregation verbose     # LACP detailed state
display interface Eth-Trunk 1        # Interface status
display interface brief              # General interface overview
```

---

### ⚙️ Optional LACP Parameters

```bash
[Huawei-Eth-Trunk1] lacp preempt enable          # Allow preemption based on priority
[Huawei-Eth-Trunk1] lacp system-priority 32768   # Lower = higher priority (default: 32768)
[Huawei-Eth-Trunk1] lacp timeout short           # Fast detection (1s intervals)
```

---

### 💾 Save Configuration

```bash
save
```

---

Here’s your **Huawei eNSP Cheatsheet – Inter-VLAN Routing** section 👇

---

### 🧠 **Inter-VLAN Routing (Router-on-a-Stick or L3 Switch)**

#### **1️⃣ Using a Router (Router-on-a-Stick)**

**Topology:** Switch ↔ Router (single physical interface with subinterfaces)

**Switch Configuration**

```bash
# Create VLANs
[SW1] vlan batch 10 20

# Assign ports to VLANs
[SW1] interface Ethernet0/0/1
[SW1-Ethernet0/0/1] port link-type access
[SW1-Ethernet0/0/1] port default vlan 10
[SW1-Ethernet0/0/1] quit

[SW1] interface Ethernet0/0/2
[SW1-Ethernet0/0/2] port link-type access
[SW1-Ethernet0/0/2] port default vlan 20
[SW1-Ethernet0/0/2] quit

# Configure trunk towards router
[SW1] interface Ethernet0/0/3
[SW1-Ethernet0/0/3] port link-type trunk
[SW1-Ethernet0/0/3] port trunk allow-pass vlan 10 20
```

**Router Configuration**

```bash
# Enable subinterfaces (one per VLAN)
[R1] interface GigabitEthernet0/0/0.10
[R1-GigabitEthernet0/0/0.10] encapsulation dot1q 10
[R1-GigabitEthernet0/0/0.10] ip address 192.168.10.1 255.255.255.0
[R1-GigabitEthernet0/0/0.10] quit

[R1] interface GigabitEthernet0/0/0.20
[R1-GigabitEthernet0/0/0.20] encapsulation dot1q 20
[R1-GigabitEthernet0/0/0.20] ip address 192.168.20.1 255.255.255.0
[R1-GigabitEthernet0/0/0.20] quit
```

🧩 **Test:**

- PCs in VLAN 10 → IP 192.168.10.x / GW 192.168.10.1
    
- PCs in VLAN 20 → IP 192.168.20.x / GW 192.168.20.1
    
- `ping` between VLANs should work ✅
    

---

#### **2️⃣ Using a Layer 3 Switch (Inter-VLAN via SVI)**

**Switch Configuration**

```bash
# Create VLANs
[SW1] vlan batch 10 20

# Assign access ports
[SW1] interface Ethernet0/0/1
[SW1-Ethernet0/0/1] port link-type access
[SW1-Ethernet0/0/1] port default vlan 10
[SW1-Ethernet0/0/1] quit

[SW1] interface Ethernet0/0/2
[SW1-Ethernet0/0/2] port link-type access
[SW1-Ethernet0/0/2] port default vlan 20
[SW1-Ethernet0/0/2] quit

# Create VLAN Interfaces (SVIs)
[SW1] interface Vlanif10
[SW1-Vlanif10] ip address 192.168.10.1 255.255.255.0
[SW1-Vlanif10] quit

[SW1] interface Vlanif20
[SW1-Vlanif20] ip address 192.168.20.1 255.255.255.0
[SW1-Vlanif20] quit

# Enable IP routing (important!)
[SW1] ip routing
```

🧠 **Tip:**  
Layer 3 switch inter-VLAN routing is faster and doesn’t need a router.


---

## 🧭 **Dynamic Routing Protocols (OSPF / RIP / BGP)**

---

### 🐍 **RIP (Routing Information Protocol)**

**1️⃣ Enable RIP and Add Networks**

```bash
[R1] rip 1
[R1-rip-1] version 2
[R1-rip-1] network 10.0.0.0
[R1-rip-1] network 192.168.1.0
[R1-rip-1] undo summary
```

**2️⃣ Optional Commands**

```bash
[R1-rip-1] undo auto-summary        # Disable automatic summarization
[R1-rip-1] silent-interface GigabitEthernet0/0/1   # Disable RIP updates on specific interface
[R1-rip-1] import-route static       # Redistribute static routes
```

**3️⃣ Verification**

```bash
[R1] display rip 1 brief
[R1] display ip routing-table protocol rip
```

---

### 🦉 **OSPF (Open Shortest Path First)**

**1️⃣ Enable OSPF**

```bash
[R1] ospf 1 router-id 1.1.1.1
```

**2️⃣ Define Networks and Areas**

```bash
[R1-ospf-1] area 0
[R1-ospf-1-area-0.0.0.0] network 10.0.0.0 0.0.0.255
[R1-ospf-1-area-0.0.0.0] network 192.168.1.0 0.0.0.255
```

**3️⃣ Optional Commands**

```bash
[R1-ospf-1] silent-interface GigabitEthernet0/0/1     # Disable hello packets
[R1-ospf-1] import-route static                        # Redistribute static
[R1-ospf-1] import-route rip                           # Redistribute RIP
```

**4️⃣ Verification**

```bash
[R1] display ospf peer
[R1] display ospf interface
[R1] display ospf routing
```

**💡Tip:** Always configure unique `router-id` on each router.

---

### 🦈 **BGP (Border Gateway Protocol)**

**1️⃣ Enable BGP and Define AS**

```bash
[R1] bgp 65001
[R1-bgp] router-id 1.1.1.1
```

**2️⃣ Create Neighbor Relationship**

```bash
[R1-bgp] peer 10.0.0.2 as-number 65002
```

**3️⃣ Advertise Networks**

```bash
[R1-bgp] ipv4-family unicast
[R1-bgp-af-ipv4] network 192.168.10.0 255.255.255.0
```

**4️⃣ Verification**

```bash
[R1] display bgp peer
[R1] display bgp routing-table
[R1] display bgp summary
```

**⚙️ Optional Commands**

```bash
[R1-bgp] peer 10.0.0.2 description LINK_TO_R2
[R1-bgp] peer 10.0.0.2 password Cisco123
[R1-bgp] peer 10.0.0.2 ebgp-max-hop 2   # for multi-hop peering
```

---

Perfect — here’s your **Huawei eNSP Cheatsheet – VRRP (Virtual Router Redundancy Protocol)** section 👇  

---

## 🛡️ **VRRP (Virtual Router Redundancy Protocol)**  

### 🎯 **Purpose:**  
VRRP provides **gateway redundancy** — if one router fails, another automatically takes over as the default gateway.

---

### 🧱 **1️⃣ Topology Example**
- Two routers connected to the same LAN  
- VLAN or interface: `192.168.10.0/24`  
- Virtual IP (shared): `192.168.10.254`

---

### ⚙️ **2️⃣ Configuration on Router 1 (Master)**
```bash
[R1] interface GigabitEthernet0/0/0
[R1-GigabitEthernet0/0/0] ip address 192.168.10.1 255.255.255.0
[R1-GigabitEthernet0/0/0] vrrp vrid 1 virtual-ip 192.168.10.254
[R1-GigabitEthernet0/0/0] vrrp vrid 1 priority 120
[R1-GigabitEthernet0/0/0] vrrp vrid 1 preempt-mode enable
```

---

### ⚙️ **3️⃣ Configuration on Router 2 (Backup)**
```bash
[R2] interface GigabitEthernet0/0/0
[R2-GigabitEthernet0/0/0] ip address 192.168.10.2 255.255.255.0
[R2-GigabitEthernet0/0/0] vrrp vrid 1 virtual-ip 192.168.10.254
[R2-GigabitEthernet0/0/0] vrrp vrid 1 priority 100
[R2-GigabitEthernet0/0/0] vrrp vrid 1 preempt-mode enable
```

---

### 🔍 **4️⃣ Verification**
```bash
[R1] display vrrp
[R2] display vrrp
```

Perfect 👌 here’s your **Huawei eNSP Cheatsheet – DHCP & DHCP Relay** section 👇  

---

## 📦 **DHCP (Dynamic Host Configuration Protocol)**  

---

### 🧱 **1️⃣ DHCP Server Configuration**

**Example Topology:**  
- Router = DHCP Server  
- VLAN 10 → 192.168.10.0/24  

```bash
[R1] ip pool VLAN10
[R1-ip-pool-VLAN10] network 192.168.10.0 mask 255.255.255.0
[R1-ip-pool-VLAN10] gateway-list 192.168.10.1
[R1-ip-pool-VLAN10] dns-list 8.8.8.8
[R1-ip-pool-VLAN10] excluded-ip-address 192.168.10.1 192.168.10.10
[R1-ip-pool-VLAN10] quit

[R1] interface Vlanif10
[R1-Vlanif10] ip address 192.168.10.1 255.255.255.0
[R1-Vlanif10] dhcp select global
```

**Verification**
```bash
[R1] display ip pool VLAN10 used
[R1] display dhcp server statistics
```

---

### 🌉 **2️⃣ DHCP Relay Configuration**

**Purpose:**  
Used when DHCP Server is on another network — the relay forwards requests to it.

**Example:**  
- SW1 (Relay) connects VLAN10 → Router DHCP Server  
- DHCP Server IP: 10.0.0.1  

**On SW1 (Relay Agent):**
```bash
[SW1] interface Vlanif10
[SW1-Vlanif10] ip address 192.168.10.1 255.255.255.0
[SW1-Vlanif10] dhcp select relay
[SW1-Vlanif10] dhcp relay server-ip 10.0.0.1
```

**On R1 (DHCP Server):**
```bash
[R1] ip pool VLAN10
[R1-ip-pool-VLAN10] network 192.168.10.0 mask 255.255.255.0
[R1-ip-pool-VLAN10] gateway-list 192.168.10.1
[R1-ip-pool-VLAN10] dns-list 8.8.8.8
[R1-ip-pool-VLAN10] quit

[R1] interface GigabitEthernet0/0/0
[R1-GigabitEthernet0/0/0] ip address 10.0.0.1 255.255.255.0
[R1-GigabitEthernet0/0/0] dhcp select global
```

**Verification**
```bash
[SW1] display dhcp relay statistics
[R1] display ip pool VLAN10 used
```


---

## 🧱 **iStack (Switch Stacking / Empilement)**

### 🎯 **Purpose:**

- Combine **two or more switches** into **one logical switch**
    
- Simplifies management (one configuration, one control plane)
    
- Provides **high availability** and **link redundancy**
    

---

### ⚙️ **1️⃣ Hardware Requirements**

- Switches must be **same model & version**
    
- Connected with **stack cables** (via stack ports or 10G interfaces)
    

---

### 🧩 **2️⃣ Basic Configuration Steps**

#### 🅰️ On both switches

Enable stack function and assign **member ID + priority**

**Switch 1 (Master)**

```bash
[SW1] stack
[SW1-stack] stack member 1 renumber 1
[SW1-stack] stack member 1 priority 255
```

**Switch 2 (Backup)**

```bash
[SW2] stack
[SW2-stack] stack member 1 renumber 2
[SW2-stack] stack member 2 priority 200
```

_(Reboot required after renumbering)_

```bash
<SW1> reboot
<SW2> reboot
```

---

### 🧬 **3️⃣ Configure Stack Ports**

Stack links are physical interfaces that connect switches together.

```bash
[SW1] stack
[SW1-stack] port 1/0/48 enable     # example 10G port for stacking
[SW1-stack] port 1/0/47 enable
[SW1-stack] quit
```

After connecting the cables (cross between the same stack ports on both), the switches will automatically form one logical device.

---

### 🔍 **4️⃣ Verification**

After reboot and cable connection:

```bash
[SW1] display stack
[SW1] display stack topology
[SW1] display version
```

You should see:

- **Member 1 → Master**
    
- **Member 2 → Standby**
    
- Shared configuration and MAC address
    

---
