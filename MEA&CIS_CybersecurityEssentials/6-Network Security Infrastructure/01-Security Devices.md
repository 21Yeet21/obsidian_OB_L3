
---

# **6.1.2 Firewalls**

A firewall enforces an **access control policy** between networks.  
All traffic entering or leaving a protected network must pass through the firewall.

### **Firewall Operation**

Typical rules include:

**Allowed traffic**

- External → Web server
    
- External → FTP server
    
- External → SMTP server
    
- Internal IMAP traffic
    

**Blocked traffic**

- Inbound traffic with internal/private IPs
    
- Inbound traffic to internal hosts
    
- ICMP echo requests
    
- Active Directory queries
    
- MS SQL queries
    
- Local broadcast traffic
    

### **Common Firewall Properties**

- Resistant to network attacks
    
- All traffic flows through the firewall (single choke point)
    
- Enforces organization’s access control policy
    

---

# **6.1.3 Common Security Architectures**

Firewall designs decide **what interfaces are trusted** and how traffic flows.

### **Private vs Public (Two-Interface Firewall)**

- **Private (inside)** = trusted
    
- **Public (outside)** = untrusted
    

**Rules**

- Inside → Outside: permitted + inspected
    
- Outside → Inside: blocked (unless exceptions defined)
    

---

# **6.1.4 Firewall Type Descriptions**

### **Packet-Filtering Firewall (Stateless)**

- Filters at **Layer 3 + Layer 4**
    
- Makes decisions using:
    
    - Source/destination IP
        
    - Protocol
        
    - Source/destination port
        
    - TCP flags (e.g., SYN)
        

### **Other Firewall Types**

- **Host-based firewall** → software on PC/server
    
- **Transparent firewall** → filters traffic between bridged interfaces
    
- **Hybrid firewall** → mixes multiple firewall types
    


---

# **6.1.6 Intrusion Prevention and Detection Devices**

IDS/IPS detect or stop malicious network activity using **signatures** and **traffic analysis**.

### **Common IDS/IPS Characteristics**

- Deployed as sensors
    
- Detect atomic (single packet) or composite (multi-packet) attacks
    
- Compare traffic patterns to known signatures
    ![[Pasted image 20251113192403.png]]

### **IPS Workflow**

1. Malicious traffic enters the network
    
2. Routed to IPS sensor
    
3. IPS blocks threat
    
4. Logs sent to management console
    
5. Traffic is dropped ("bit bucket")
    

### **IDS/IPS Deployment Options**

- Router with Cisco IOS IPS
    
- Dedicated IDS/IPS appliance
    
- Security module in ASA, switch, or router
    

---

# **6.1.7 IDS vs IPS — Advantages & Disadvantages**

### **IDS Advantages**

- Off-path → no impact on network performance
    
- Failsafe: if sensor dies, traffic still flows
    

### **IDS Disadvantages**

- Cannot stop malicious packets
    
- High tuning effort required
    
- Easier to evade (not inline)
    

---

# **6.1.8 Types of IPS**

There are two primary IPS types:

---

## **Host-Based IPS (HIPS)**

Software installed on the host.

### **Benefits**

- OS-specific protection
    
- Monitors registry, system files, processes
    
- Protects after decryption
    
- Acts like AV + anti-malware + firewall combined
    

### **Drawbacks**

- OS-dependent
    
- Must be installed on all hosts
    
- Only protects locally (no full network visibility)
    

---

## **Network-Based IPS (NIPS)**

Dedicated/embedded sensors monitoring network traffic.

### **Benefits**

- Stops attacks in real time
    
- Monitors entire network segments
    
- Essential for layered defense
    

Sensors are placed at key network points (DMZ, core, WAN edge, etc.).

---

# **6.1.9 Specialized Security Appliances**

### **Cisco AMP (Advanced Malware Protection)**

Provides protection **before, during, and after** an attack.

**Before**

- Detects known and emerging threats
    
- Strengthens defenses
    

**During**

- Blocks malicious files
    
- Stops exploit attempts
    

**After**

- Continuous file monitoring
    
- Detects files that later show malicious behavior
    
- Shows infection path and affected systems
    

Powered by **Cisco Talos**, one of the largest threat intelligence networks globally.

---
