
---

# **9.3.1 Host-Based Firewalls — Summary**

Host-based firewalls are software firewalls installed directly on an endpoint (PC, laptop, tablet, mobile). They inspect inbound and outbound traffic and enforce rules at the host level.

### **Key points**

- Control traffic entering or leaving the device
    
- Use predefined **profiles** (policies) or custom rule sets
    
- Rules can filter by **IP address, port, protocol**
    
- Can alert users when suspicious activity appears
    
- Logs include:
    
    - Date/time
        
    - Allowed/denied action
        
    - Source/destination IP
        
    - Source/destination ports
        
    - Routine events (DNS queries, etc.)
        

Because logs can be very long, analysts use filtering or parsing to analyze them.

### **Distributed firewalls**

A distributed firewall system:

- Runs agents on hosts
    
- Uses a central management system to push rules and collect logs
    
- Provides consistent security across all endpoints
    

### **Examples of host-based firewalls**

- **Windows Defender Firewall**
    
    - Profiles: Public, Private, Domain
        
    - Supports logging
        
    - Centrally managed through Group Policy
        
- **iptables (Linux)**
    
    - Kernel-level packet filtering using Netfilter
        
- **nftables (Linux)**
    
    - Successor to iptables
        
    - Uses a virtual machine in the kernel for packet evaluation
        
- **TCP Wrappers (Linux)**
    
    - Rule-based access control and logging based on service/IP
        

---

# **9.3.2 Host-Based Intrusion Detection (HIDS) — Summary**

HIDS monitors and protects the host from known and unknown threats. It is more advanced than a simple antivirus because it includes:

- Log analysis
    
- Integrity checking
    
- Policy enforcement
    
- Rootkit detection
    
- Correlation of events
    
- Alerting
    

HIDS is **agent-based**, meaning the software runs locally on each protected host. A centralized **HIDS Management Server** collects logs and alerts from agents.

### **HIDS = Antivirus + Host Firewall + Intrusion Analysis**

A HIDS can:

- Detect malware
    
- Prevent execution of known threats
    
- Report suspicious system behavior
    

### **Architecture**

A typical HIDS setup includes:

- Multiple hosts running HIDS agents
    
- Central HIDS manager collecting logs and alerts
    
- Security team analyzing results
    

---

# **9.3.3 HIDS Operation — Summary**

HIDS works using both **proactive** and **reactive** techniques.

### ✔️ **Proactive — Signature-based detection**

- Detects **known** malware based on signatures
    
- Cannot detect zero-day or polymorphic malware
    

### ✔️ **Reactive — Behavior/Anomaly/Policy-based detection**

**1. Anomaly Detection**

- Builds a baseline of normal activity (CPU use, processes, user behavior)
    
- Flags significant deviations
    
- Can generate false positives if normal behavior changes
    

**2. Policy/Rule-Based Detection**

- Uses predefined or custom rules
    
- Detects violations of expected behavior
    
- Can automatically stop malicious processes, log events, and alert security staff
    

---

# **9.3.4 HIDS Products — Summary**

Several HIDS solutions exist, often combining detection with centralized management and automated response.

### **Examples**

- **Cisco AMP for Endpoints**
    
- **AlienVault USM**
    
- **Tripwire**
    
- **OSSEC (Open Source HIDS SECurity)** — major open-source option
    

### **OSSEC Features**

- Uses agents installed on hosts (Windows, macOS, Linux, Solaris)
    
- Central manager receives events and alerts
    
- Supports:
    
    - Log monitoring
        
    - File integrity monitoring
        
    - Rootkit detection
        
    - Syslog integration with network devices
        
    - Automated responses (run scripts on hosts)
        

---

If you're ready, we can continue with **9.4 (Endpoint Protection Schemes)** or the next module.