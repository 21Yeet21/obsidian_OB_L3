
#### 🔹 Router-on-a-Stick (RoS)

- **Definition**: One physical router interface handles multiple VLANs using **sub-interfaces**.
    
    - Example: `G0/0.10` for VLAN 10, `G0/0.20` for VLAN 20.
        
- **Disadvantage**: All traffic goes through a single interface → **reduced bandwidth**.
    
    - Example: If the link is 1 Gbps and you have 3 VLANs, they all share that same 1 Gbps.
        
- **Interface Requirement**: Must be the **same technology** on both sides.
    
    - Example: Router GigabitEthernet ↔ Switch GigabitEthernet (not GE ↔ Serial).
        

#### 🔹 Router Technologies

- A router can connect **different technologies**.
    
    - Example: One interface runs **Ethernet** for LAN, another runs **PPP over Serial** for WAN.
        
- Command `[R] arp broadcast enable`: Allows ARP requests to be broadcasted in that interface’s domain.
    
    - Example: PC1 sends ARP → router forwards ARP request → PC2 replies.
        

#### 🔹 Switch Types

**1. L2 Switch (Access Switch)**

- Works at **Layer 2 (MAC addresses)**.
    
- Has a **management IP** (used for SSH, Telnet, or Web access).
    
    - Example: Switch IP = 192.168.1.2/24 → only for managing the switch.
        
- **Cannot route** between VLANs (needs a router or L3 switch).
    

**2. L3 Switch (Multilayer Switch)**

- Can do **Inter-VLAN routing** directly, without a router-on-a-stick.
    
    - Example: VLAN 10 (192.168.10.0/24) ↔ VLAN 20 (192.168.20.0/24).
        
- Creates **multiple broadcast domains** by routing between VLANs.
    
- **MAC Address behavior**:
    
    - Old routers (RoS): all sub-interfaces used **the same MAC address**.
        
    - New routers (RoS): each sub-interface can have its **own virtual MAC address**.
        
    - L3 Switch: usually uses **a single MAC address** for all routed VLANs.
        

---






