
---

# **5.2.2 Wireless Security Overview**

Wireless LANs are inherently exposed because anyone within range of the AP can attempt to connect. Attackers don’t need physical access — only a wireless NIC and basic knowledge of cracking tools.

### **Main Wireless Threats**

- **Interception of data**  
    • Wireless traffic must be encrypted to prevent eavesdropping.
    
- **Wireless intruders**  
    • Unauthorized users may try to connect; strong authentication reduces this risk.
    
- **DoS attacks**  
    • WLAN service can be disrupted intentionally or accidentally.
    
- **Rogue Access Points**  
    • Unauthorized APs create backdoors into the network.
    

---

# **5.2.3 DoS Attacks**

Wireless DoS attacks can come from:

### **1. Misconfigured devices**

- Accidental misconfiguration can disable an AP or the entire WLAN.
    
- Admins with malicious intent can also intentionally disrupt services.
    

### **2. Malicious interference**

- Attackers can jam or flood wireless channels to make the WLAN unusable.
    

### **3. Accidental interference**

- Devices such as:
    
    - Microwave ovens
        
    - Cordless phones
        
    - Baby monitors
        
    - Bluetooth devices
        
- These especially affect the **2.4 GHz band**.
    

### **Mitigation**

- Harden and secure device configurations.
    
- Use strong passwords + backup configs.
    
- Perform changes during off-hours.
    
- Monitor RF interference; use **5 GHz** when possible.
    

---

# **5.2.4 Rogue Access Points**

A **rogue AP** is any unauthorized AP connected to the corporate network.

### **Why it’s dangerous**

- Provides attackers an entry point into the wired LAN.
    
- Allows traffic capture (packets, MAC addresses).
    
- Can be used for MITM attacks.
    
- Users can unintentionally create one (e.g., making a Windows laptop a Wi-Fi hotspot).
    

### **Prevention**

- Configure WLCs with **rogue AP detection policies**.
    
- Continuously monitor the RF spectrum for unauthorized devices.
    
- Enforce strict corporate rules about adding wireless equipment.
    

---

# **5.2.5 Man-in-the-Middle (MITM) Attacks**

Attackers place themselves between a victim and the legitimate AP to intercept and modify traffic.

### **Evil Twin Attack (most common wireless MITM)**

- Attacker sets up a rogue AP with:
    
    - The same **SSID** as the legitimate AP
        
    - Open or weak authentication
        
    - Stronger signal than the real AP
        
- Victims connect to the attacker’s AP without realizing it.
    
- The rogue AP forwards traffic to the real AP, allowing:
    
    - Password theft
        
    - Session hijacking
        
    - Device compromise
        
    - Data interception
        

### **Defending Against MITM**

- Authenticate all devices (use WPA2/WPA3, 802.1X).
    
- Monitor the WLAN for abnormal MAC addresses or unknown APs.
    
- Use wireless intrusion detection (WIDS/WIPS).
    
- Prefer encrypted channels and avoid open public Wi-Fi when possible.
    

---
