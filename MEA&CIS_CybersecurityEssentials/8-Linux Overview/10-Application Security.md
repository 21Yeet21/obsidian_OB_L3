
# **9.4.1 Attack Surface — Summary**

A **vulnerability** is a weakness that can be exploited.  
The **attack surface** is the total collection of all weaknesses that an attacker can reach and exploit in a system.

An attack surface can include:

- **Open ports** on hosts and servers
    
- **Internet-facing software** and exposed services
    
- **Wireless protocols** (Wi-Fi, Bluetooth, IoT protocols)
    
- **Users themselves** (social engineering, insider misuse)
    

As organizations adopt more devices and cloud services, the attack surface continuously **expands**. IoT devices, BYOD, mobile devices, and cloud workloads all contribute to more entry points for attackers.

### **SANS Institute — Three Attack Surface Components**

1. **Network Attack Surface**
    
    - Vulnerabilities in wired and wireless protocols
        
    - IoT wireless protocols (Zigbee, Bluetooth, NFC)
        
    - Network and transport layer vulnerabilities
        
2. **Software Attack Surface**
    
    - Web applications
        
    - Cloud services
        
    - Host-based applications and APIs
        
    - Any software exposed to users or the internet
        
3. **Human Attack Surface**
    
    - User mistakes
        
    - Social engineering
        
    - Insider threats
        
    - Weak passwords, poor security habits
        

---

# **An Expanding Attack Surface — Summary**

Modern networks face rapid expansion in threats because **more systems and devices are online than ever before**.

The figure highlights the key drivers:

### **IoT**

- Number of IoT devices projected to reach **30+ billion**
    
- More devices = more vulnerabilities
    

### **Cloud**

- **92%** of workloads moving to cloud data centers
    
- Expands exposure due to external hosting and shared infrastructures
    

### **BYOD**

- **70%** of professionals work from their own personal devices
    
- Personal devices often lack enterprise-level protection
    

### **Mobility**

- **20% of all IP traffic** will originate from mobile devices
    
- Mobile platforms introduce unique security challenges
    

### **Global Operations**

- Worldwide IP traffic expected to **triple within five years**
    
- More traffic → more attack vectors and opportunities for attackers
    

---

# **9.4.2 Application Block List and Allow List — Summary**

One of the most effective ways to reduce an endpoint’s attack surface is by **controlling which applications can run**.
![[Pasted image 20251121184412.png]]
### **Blocklisting (Blacklist)**

- A _block list_ contains applications that are **not allowed to run**.
    
- Used to prevent known **malicious**, **vulnerable**, or **unauthorized** software from executing.
    
- Helps stop risky applications before they create vulnerabilities.

### **Allow Listing (Whitelist)**

- An _allow list_ contains applications that **are permitted** to run.
    
- Anything **not** on the allow list is automatically blocked.
    
- Far more secure because it assumes **deny-by-default**.
    

Allow lists are created based on the organization’s **security baseline**:

- Defines acceptable risk
    
- Defines which software is approved
    
- Prevents unapproved and unknown programs from executing
    

### **Website Blocklists / Allowlists**

- Websites can also be blocklisted or allowlisted
    
- Lists can be manually created or received from threat intelligence services
    
- Security systems update these lists automatically
    
- Example:
    
    - **Cisco Firepower** can obtain updated blocklists from **Cisco Talos Intelligence**
        
    - **Spamhaus Project** provides free malicious domain/IP blocklists
        

### **Windows Example**

Windows Group Policy supports:

- _“Don’t run specified Windows applications”_
    
- _“Run only specified Windows applications”_
    

---

# **9.4.3 System-Based Sandboxing — Summary**

Sandboxing isolates suspicious files in a **controlled environment** to analyze their behavior safely.

### **Why Sandboxing is Needed**

- Malware evolves rapidly (polymorphism, zero-day threats)
    
- Even with antivirus and HIDS, some malware will execute on the network
    
- Sandboxes help analysts understand:
    
    - How malware behaves
        
    - What changes it makes
        
    - How to create new signatures and detection rules
        

### **How Sandboxing Works**

1. A suspicious file is extracted (often by advanced tools like Cisco AMP).
    
2. It is executed inside a safe virtual environment (sandbox).
    
3. The sandbox records actions:
    
    - File system changes
        
    - Registry changes
        
    - Network connections
        
    - Processes created
        
    - Attempted exploitation techniques
        

### **Examples of Sandboxing Tools**

- **Cisco Threat Grid** (integrated with Cisco AMP & Firepower)
    
- **Cuckoo Sandbox** (free, open-source)
    
- **VirusTotal** (public cloud sandbox)
    
- **Joe Sandbox**
    
- **CrowdStrike Falcon Sandbox**
    
- **ANY.RUN** (interactive cloud sandbox)
    

### **ANY.RUN Features**

- Upload malware for live, interactive execution
    
- Captures screenshots of malware behavior
    
- Shows:
    
    - Network activity (HTTP, DNS, IP connections)
        
    - System changes
        
    - File hashes and hex/ASCII views
        
    - Indicators of Compromise (IOCs)
        
- Maps malware behavior to **MITRE ATT&CK tactics**
    

---

If you're ready, we can move to the **next section of the module**.