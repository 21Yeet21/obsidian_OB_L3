

---

# **4.1 – ARP, DNS, and DHCP Attacks**

---

## **4.1.1 – ARP Vulnerabilities**

### **How ARP works**

- Host sends **ARP Request (broadcast)** asking: “Who has IP X?”
    
- The correct host replies with **ARP Reply (unicast)** containing its MAC.
    
- Devices store the result in their **ARP cache**.
    

### **Gratuitous ARP**

- A device can send an **unsolicited ARP reply** to announce its MAC.
    
- Other hosts update their ARP tables automatically.
    

### **Problem**

ARP has **no authentication** → any device can claim any IP/MAC.

### **Result**

- Threat actor can send false ARP replies.
    
- Hosts update their ARP table with attacker’s MAC.
    
- Attacker becomes **Man-in-the-Middle (MiTM)**.
    
- Common goal: impersonate the **default gateway**.
    

---

## **4.1.2 – ARP Cache Poisoning**

### **Process**

1. PC-A sends ARP Request to learn the MAC of its default gateway (R1).
    
2. R1 replies → PC-A updates ARP table normally.
    
3. Threat actor sends **spoofed gratuitous ARP replies**:
    
    - “192.168.10.1 (gateway) is at EE:EE:EE:EE:EE:EE”
        
    - “192.168.10.10 (PC-A) is at EE:EE:EE:EE:EE:EE”
        
4. Both PC-A and R1 update their ARP tables → traffic passes through attacker.
    ![[Pasted image 20251113183704.png]]

### **Types of ARP poisoning**

- **Passive** – attacker only sniffs data.
    
- **Active** – attacker modifies packets or injects malicious data.
    

### **Common ARP attack tools**

- **dsniff**
    
- **Ettercap**
    
- **Cain & Abel**
    
- **Yersinia**
    

---

## **4.1.3 – DNS Attacks**

DNS is critical and often poorly secured.

### **Common DNS Attack Types**

- **DNS open resolver attacks**
    
- **DNS stealth attacks**
    
- **DNS domain shadowing**
    
- **DNS tunneling**
    

---

### **1. DNS Open Resolver Attacks**

#### **a. DNS Cache Poisoning**

Threat actor sends fake DNS records → redirects users to malicious sites.

#### **b. DNS Reflection / Amplification**

Threat actor:

- Spoofs victim's IP
    
- Sends DNS queries to open resolvers
    
- Resolvers send large replies to victim → DoS/DDoS
    

#### **c. Resource Exhaustion**

Flooding the DNS resolver with queries → makes it crash or reboot.

---

### **2. DNS Stealth Techniques**

#### **Fast Flux**

- Constantly changing DNS IP addresses to hide malicious sites.
    

#### **Double Flux**

- Rotates both:
    
    - Hostname → IP
        
    - Authoritative name servers
        
- Harder to track attackers.
    

#### **DGA (Domain Generation Algorithms)**

- Malware rapidly generates random domain names to contact C2 servers.
    

---

### **3. DNS Domain Shadowing**

- Attacker steals domain account credentials.
    
- Creates many hidden subdomains pointing to malicious servers.
    
- Owner of the domain is unaware.
    

---

## **4.1.4 – DNS Tunneling**

Threat actor hides non-DNS data inside DNS queries.

### **How DNS tunneling works**

1. Data is split into many small encoded chunks.
    
2. Chunks inserted into DNS query labels.
    
3. Queries reach the attacker’s **authoritative DNS server**.
    
4. Authoritative server responds with encoded commands (e.g., in a TXT record).
    
5. Malware on infected host rebuilds the commands and executes them.
    

### **Purpose**

- Exfiltrate data
    
- Command & Control (C2)
    
- Bypass firewalls (DNS almost always allowed)
    

### **Detection**

- Long or weird domain names
    
- Large number of TXT or NULL queries
    
- Use DNS security solutions (e.g., **Cisco Umbrella**)
    

---

## **4.1.5 – Normal DHCP Operation**

Process:

1. **DHCPDISCOVER** (broadcast) → “Anyone give me an IP?”
    
2. **DHCPOFFER** (unicast) → IP, mask, gateway, DNS, lease time
    
3. **DHCPREQUEST** (broadcast) → “I accept this offer”
    
4. **DHCPACK** (unicast) → final confirmation
    

---

## **4.1.6 – DHCP Attacks**

### **DHCP Spoofing Attack**

Threat actor connects a **rogue DHCP server** to the network.

### **What the rogue server can do**

- **Fake default gateway** → MiTM
    
- **Fake DNS server** → redirect to malicious sites
    
- **Invalid IP configuration** → DoS the client
    

### **Attack steps**

1. Client sends **DHCPDISCOVER**.
    
2. Both real and rogue DHCP servers reply.
    
3. Client accepts the **first DHCPOFFER** received.
    
4. If the rogue server responds faster:
    
    - Client gets malicious IP settings.
        
    - Attacker controls traffic or breaks connectivity.
        

---

