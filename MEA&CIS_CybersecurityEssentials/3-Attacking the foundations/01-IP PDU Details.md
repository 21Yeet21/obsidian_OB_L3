
---

# **3.1 — IPv4 & IPv6 Packet Headers (Security Focus)**

## **3.1.1 — IPv4 and IPv6 Overview**

- IP is a **Layer 3, connectionless** protocol.
    
- IP **does not validate source IP addresses** → easy for threat actors to spoof IPs.
    
- Attackers can also tamper with header fields → understanding headers is essential for security analysts.
    
- IPv4 and IPv6 headers contain fields that can be abused for:
    
    - **Spoofing**
        
    - **Fragmentation attacks**
        
    - **Traffic manipulation**
        
    - **Evasion techniques**
        

---

# **3.1.2 — IPv4 Header (20 bytes minimum)**

## **IPv4 Header Fields (with security notes)**
![[Pasted image 20251113163518.png]]

- **Version (4 bits)**  
    → Always `0100` (IPv4).
    
- **IHL – Internet Header Length (4 bits)**  
    → Indicates header size (min 20 bytes).  
    _Used in evasion attacks by modifying header size._
    
- **DS (Differentiated Services) – 8 bits**
    
    - **DSCP (6 bits)** → QoS marking
        
    - **ECN (2 bits)** → Congestion notification  
        _Attackers may modify DSCP to prioritize malicious traffic._
        
- **Total Length (16 bits)**  
    → Entire packet size (max 65,535 bytes).  
    _Used in fragmentation attacks._
    
- **Identification, Flags, Fragment Offset**  
    → Used for fragmentation and reassembly.  
    _Core of fragmentation attacks (Teardrop, overlapping fragments, IDS evasion)._
    
- **TTL – Time To Live (8 bits)**  
    → Decrements by 1 per router.
    
    - TTL = 0 → packet dropped + ICMP Time Exceeded.  
        _Attackers manipulate TTL for reconnaissance (OS fingerprinting)._
        
- **Protocol (8 bits)**  
    → Identifies Layer 4 protocol.
    
    - ICMP = 1
        
    - TCP = 6
        
    - UDP = 17
        
- **Header Checksum (16 bits)**  
    → Error-checking for the header only.  
    _Tampering requires recomputation (attackers know this)._
    
- **Source IP Address (32 bits)**  
    → Always unicast.  
    _Spoofing is common in DDoS._
    
- **Destination IP Address (32 bits)**  
    → Target IP.
    
- **Options (variable)**  
    → Padding used if needed.  
    _Rarely used; often blocked for security._
    

---

# **3.1.4 — IPv6 Header (Fixed 40 bytes)**

IPv6 simplifies and strengthens many header functions.
![[Pasted image 20251113163702.png]]
## **IPv6 Header Fields**

- **Version (4 bits)**  
    → Always `0110` (IPv6).
    
- **Traffic Class (8 bits)**  
    → QoS (similar to DSCP/ECN).
    
- **Flow Label (20 bits)**  
    → Identifies a flow; routers treat similar packets consistently.  
    _Useful for QoS but can be abused in evasion._
    
- **Payload Length (16 bits)**  
    → Size of the actual data (not including the header).
    
- **Next Header (8 bits)**  
    → Similar to IPv4 Protocol field.  
    → Points to upper-layer protocol _or_ to Extension Headers.
    
- **Hop Limit (8 bits)**  
    → Same role as IPv4 TTL.
    
- **Source IPv6 Address (128 bits)**
    
- **Destination IPv6 Address (128 bits)**
    

---

## **IPv6 Extension Headers (EH)**

- Optional fields inserted between header and payload.
    
- Used for:
    
    - Fragmentation
        
    - Security
        
    - Mobility
        
    - Routing
        
- **Important: routers do NOT fragment IPv6 packets.**  
    → Fragmentation only done by the sending host.
    

_Attackers sometimes abuse EHs to bypass security controls or confuse firewalls._

---

If you want, I can continue with **3.2**, or produce a **full clean summary of Module 3** for Obsidian.