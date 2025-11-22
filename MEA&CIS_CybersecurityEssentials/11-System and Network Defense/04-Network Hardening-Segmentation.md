
---

# **12.4.2 Virtual Local Area Networks (VLANs)**

### **Devices are grouped**

- VLANs group devices logically, not physically.
    
- Each switch port can be assigned to a specific VLAN.
    
- Switch-to-switch links that carry multiple VLANs are **trunks**.
    

### **The network is segmented**

- VLANs segment the LAN by department, project, function, or sensitivity.
    
- Devices inside a VLAN behave like they’re on a separate network, even if physically on the same switch.
    
- HR VLAN example: isolates sensitive personnel data.
    
- Trunks allow the same VLAN to span multiple switches.
    

### **Data is protected**

- VLANs limit broadcast domains and reduce unnecessary traffic.
    
- Security requires: performance monitoring, advanced configuration (like pruning, allowed VLAN lists), and regular patching.
    
- Cybercriminals can still attack VLANs (e.g., VLAN hopping).
    

---

# **12.4.3 The Demilitarized Zone (DMZ)**

### **How a DMZ works**

- A DMZ is a small, isolated network placed **between the internal LAN and the Internet**.
    
- Public-facing servers (web, mail, DNS) are hosted here so external users can reach them without exposing the internal network.
    

### **Risk zones**

Organizations typically have multiple risk zones:

- **LAN (trusted)** → low risk, high trust
    
- **Extranet** → medium-low risk, medium-high trust
    
- **DMZ** → medium-high risk, medium-low trust
    
- **Internet** → highest risk, lowest trust
    

### **Traffic control**

- Firewalls control **north-south traffic** (in/out of the network).
    
- Firewalls also control **east-west traffic** (between internal servers).
    

### **Zero Trust**

- Traditional networks trust internal users too much.
    
- Zero Trust means: **trust no one by default, verify everything continuously** — regardless of user role, device, or location.
    

---

