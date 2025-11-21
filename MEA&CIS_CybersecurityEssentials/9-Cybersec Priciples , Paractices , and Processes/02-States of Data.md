
---

# **10.2 — Protecting Data in All States**

Cybersecurity requires protecting data **at rest**, **in transit**, and **in process**.  
Below is the complete summary for each subsection.

---

# **10.2.2 Data at Rest**

**Data at rest = stored data**  
(Not being accessed, transmitted, or processed.)

It may be stored on:

### **1. Direct-Attached Storage (DAS)**

- Storage physically connected to a computer
    
- Example: Hard drive, USB
    
- Not shared by default
    
- Hard to manage, easier to attack if host is compromised
    

### **2. RAID (Redundant Array of Independent Disks)**

- Combines multiple disks into one
    
- Improved performance + fault tolerance
    
- Often used in servers
    

### **3. NAS (Network Attached Storage)**

- Storage accessible through a network
    
- Centralized, scalable, easy to add capacity
    
- Used by companies for shared storage
    

### **4. SAN (Storage Area Network)**

- High-speed network-based storage
    
- Connects multiple servers to centralized storage
    
- Enterprise-level performance
    

### **5. Cloud Storage**

- Remote data center storage (Google Drive, iCloud, Dropbox)
    
- Accessible anywhere with internet
    
- Subscription-based
    

---

# **10.2.3 Challenges of Protecting Stored Data**

**DAS Challenges**

- Hard to centrally manage
    
- Vulnerable if local host is infected
    
- Organizations should limit what is stored on DAS
    

**Network Storage Challenges (RAID, NAS, SAN)**

- More secure but more complex
    
- Handle large amounts of data → higher risk if failure occurs
    
- Need careful **configuration, testing, monitoring**
    

**Backups**

- Data at rest also includes backup files
    
- Must be protected, automated, and centrally managed
    

---

# **10.2.5 Methods of Transmitting Data (Data in Transit)**

**Data in transit = data being transferred between devices**

### **1. Sneaker Net**

- Moving data physically with USB or external drives
    
- Still used in organizations
    

### **2. Wired Networks**

- Copper or fiber optic
    
- Used for LAN/WAN
    
- High reliability and security
    

### **3. Wireless Networks**

- Radio waves
    
- Increasing use = enlarged attack surface
    
- More guest devices, more risk
    

### **4. Packets**

- All networks transmit data in packets
    
- IP, HTTP are open standards
    
- Protecting confidentiality, integrity, availability is critical
    

---

# **10.2.6 Challenges of Data in Transit**

### **1. Confidentiality Risk: Interception**

Attackers can capture data.  
**Countermeasures:**

- Encryption (SSL/TLS, IPsec, VPN)
    

### **2. Integrity Risk: Manipulation**

Attackers can alter data in transit.  
**Countermeasures:**

- Hashing
    
- Integrity checks
    
- Data redundancy
    

### **3. Availability Risk: Rogue Devices**

Attackers can impersonate Wi-Fi APs and hijack sessions.  
**Countermeasures:**

- **Mutual authentication**  
    (User authenticates server + server authenticates user)
    

---

# **10.2.7 Data in Process**

**Data in process = data currently being input, modified, or output.**  
Not in storage, not being transmitted.

---

### **1. Input Phase**

Threats:

- Incorrect data entry
    
- Wrong formats
    
- Bad sensor data
    
- Mislabeling
    

Protection:

- Validation checks
    
- Clean input processes
    
- Reliable sensors
    

---

### **2. Modification Phase**

When data is changed intentionally or unintentionally.

Examples of intended modification:

- Encoding/decoding
    
- Compression
    
- Encryption/decryption
    
- User edits
    
- System updates
    

**Threats (corruption):**

- Equipment failure
    
- Software errors
    
- Malware
    

---

### **3. Output Phase**

Sending data to output devices:

- Printers
    
- Displays
    
- Speakers
    

Accuracy is critical because output influences decisions.

Threats:

- Wrong delimiters
    
- Misconfigured printers or display settings
    
- Bad communication configurations
    

---
