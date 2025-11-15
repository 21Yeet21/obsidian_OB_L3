
---

# **3.2 — IP Vulnerabilities & Attacks**

---

## **3.2.1 — IP Vulnerabilities**

IP is vulnerable to several common attack types:

### **• ICMP-Based Attacks**

- Used for **reconnaissance**, **host discovery**, **OS fingerprinting**, and **firewall probing**.
    
- Used for **DoS floods** and manipulating routing behavior.
    

### **• DoS (Denial of Service)**

- Goal: prevent legitimate users from accessing resources.
    

### **• DDoS (Distributed DoS)**

- Large-scale, coordinated DoS from multiple machines.
    

### **• IP Spoofing**

- Threat actor forges the **source IP address**.
    
- Used for blind/non-blind spoofing, scanning, bypassing ACLs.
    

### **• Man-in-the-Middle (MiTM)**

- Attacker inserts themselves between two hosts:
    
    - Packet capture
        
    - Manipulation
        
    - Session hijacking
        

### **• Session Hijacking**

- Attacker steals an active session after gaining access to the local network.
    

---

## **3.2.2 — ICMP Attacks**

ICMP normally handles:

- Diagnostics
    
- Error reporting
    
- Connectivity testing (ping)
    

Threat actors misuse ICMP for:

### **Reconnaissance**

- Network mapping
    
- Host discovery
    
- OS fingerprinting
    
- Firewall rule testing
    

### **DoS / DDoS**

Example: **ICMP Flood Attack**

- Attacker sends large amounts of spoofed ICMP Echo Requests.
    
- Victim replies, wasting CPU, network bandwidth, and resources.
    

### **Common ICMP Messages Used in Attacks**

- **Echo Request/Reply** → pings, reconnaissance, DoS
    
- **Timestamp Request** → host discovery
    
- **Address Mask Request** → map internal networks
    
- **Redirect** → force traffic through attacker (MiTM)
    
- **Router Advertisement** → inject fake route entries
    

### **Defense**

- Strict **ICMP ACL filtering** at network edge
    
- IDS/IPS monitoring
    
- Rate limiting
    
- Disabling unnecessary ICMP types
    

---

## **3.2.4 — Amplification & Reflection Attacks**

Threat actors combine two techniques:

### **• Reflection**

- The attacker sends requests that appear to come from the victim.
    
- Third-party hosts send replies **back to the victim**.
    

### **• Amplification**

- One small request generates a **much larger reply**, increasing damage.
    
![[Pasted image 20251113174727.png]]
### **Example: Smurf Attack**

- Attacker sends ICMP Echo Requests to a broadcast address
    
- Source IP is spoofed as the **victim**
    
- All hosts reply → **massive ICMP flood** to victim
    

### **Modern amplification attacks include:**

- **DNS amplification**
    
- **NTP amplification**
    
- **SSDP amplification**
    

### **Resource Exhaustion**

- Attack consumes CPU, memory, or bandwidth until the target crashes.
    

---

## **3.2.5 — Address Spoofing Attacks**

### **IP Spoofing**

- Fake source IP address
    
- Used for:
    
    - Hiding identity
        
    - Bypassing ACLs
        
    - Session hijacking
        
    - DoS/DDoS
        

### **Types**

- **Non-blind spoofing**
    
    - Attacker can see traffic
        
    - Used for session hijacking and sequence-number prediction
        
- **Blind spoofing**
    
    - Attacker cannot see responses
        
    - Used mainly for DoS
        

---

### **MAC Address Spoofing**

Occurs on the **local network** (Layer 2).

- Attacker changes their MAC address to match a legitimate device.
    
- Switch updates its CAM table incorrectly.
    
- Traffic intended for the real device is sent to the attacker.
    

This is a classic **Layer 2 MiTM technique**.

---

### **Service Spoofing (Rogue Servers)**

- Example: **Rogue DHCP Server**
    
    - Attacker supplies victims with malicious:
        
        - Default gateway
            
        - DNS server
            
        - IP configuration
            
    - Creates full MiTM condition
        

---

