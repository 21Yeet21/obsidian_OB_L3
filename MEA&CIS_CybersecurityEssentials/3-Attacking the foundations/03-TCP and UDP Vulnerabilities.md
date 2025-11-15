
---

# **3.3 – TCP & UDP Attacks**

---

## **3.3.1 – TCP Segment Header**

TCP data appears immediately after the IP header.
![[Pasted image 20251113175444.png]]

### **Control Bits (Flags)**

- **URG** – Urgent pointer used
    
- **ACK** – Acknowledgment used
    
- **PSH** – Push function
    
- **RST** – Reset connection
    
- **SYN** – Synchronize sequence numbers
    
- **FIN** – No more data from sender
    

---

## **3.3.2 – TCP Services**

### **Reliable Delivery**

- TCP uses **ACKs** and retransmissions.
    
- Examples: HTTP, TLS, FTP, DNS zone transfers.
    

### **Flow Control**

- Multiple segments can be acknowledged at once.
    

### **Stateful Communication (3-Way Handshake)**

1. Client → Server: **SYN**
    
2. Server → Client: **SYN-ACK**
    
3. Client → Server: **ACK**
    ![[Pasted image 20251113175609.png]]

Connection established.

---

## **3.3.3 – TCP Attacks**

### **1. TCP SYN Flood**

Exploits the TCP handshake.

- Threat actor sends many **SYNs** with spoofed IPs.
    
- Server responds with **SYN-ACK** and waits.
    
- ACK never comes → **half-open connections** accumulate.
    
- Server becomes unavailable.
    ![[Pasted image 20251113175624.png]]

### **2. TCP Reset (RST) Attack**

- Threat actor sends a spoofed TCP packet with the **RST** flag.
    
- Abruptly terminates a TCP session.
    
- Can disrupt sessions of routers, VPNs, BGP, etc.
    

### **3. TCP Session Hijacking**

- Attacker takes over an **already authenticated** TCP session.
    
- Requirements:
    
    - Spoof the victim’s IP
        
    - Predict the next **sequence number**
        
    - Send a forged ACK
        
- Attacker can send data to the target (but cannot receive responses).
    

---

## **3.3.4 – UDP Segment Header & Operation**

### **UDP Header Fields**

- **Source Port (16 bits)**
    
- **Destination Port (16 bits)**
    
- **Length (16 bits)**
    
- **Checksum (16 bits — optional)**
    
- **Application Data**
    

### **Characteristics**

- Connectionless
    
- Low overhead
    
- No sequencing, no retransmission, no flow control
    
- Used by:
    
    - DNS, DHCP, TFTP
        
    - NFS, SNMP
        
    - Streaming, VoIP
        

---

## **3.3.5 – UDP Attacks**

### **Lack of Encryption**

- UDP has **no default encryption**.
    
- Anyone on the path can:
    
    - Read packets
        
    - Modify data
        
    - Recalculate checksum (if used)
        
- But tampering attacks are **rare**.
    

### **UDP Flood Attack**

Most common UDP attack.

**How it works:**

1. Threat actor uses tools:
    
    - **UDP Unicorn**
        
    - **LOIC**
        
2. Sends massive UDP packets (often spoofed).
    
3. Server receives packets on **many random ports**.
    
4. Most ports are closed → server replies with:
    
    - **ICMP Port Unreachable**
        
5. High number of ICMP replies → bandwidth and CPU get saturated.
    

**Result:**  
A **DoS** similar to ICMP floods.

---

