
---

# **5.3.3 802.11 Original Authentication Methods**

Early WLAN authentication relied on two simple methods:

### **1. Open System Authentication**

- No password required.
    
- Any client can associate freely.
    
- Used for public Wi-Fi (cafes, airports, hotels).
    
- Security must be handled by the **client** (e.g., VPN).
    

### **2. Shared Key Authentication**

- Requires a pre-shared password.
    
- Implemented using WEP → later WPA → WPA2 → WPA3.
    
- Provides authentication + encryption between client and AP.
    

### **Weakness**

- SSID hiding and MAC filtering **do not** provide real security.
    
- SSIDs can be discovered easily; MAC addresses can be spoofed.
    

---

# **5.3.4 Shared Key Authentication Methods**

Shared key authentication evolved through the following standards:

### **WEP**

- First encryption method; weak and easily broken.
    

### **WPA**

- Patch to fix WEP weaknesses.
    
- Uses **TKIP** encryption.
    

### **WPA2**

- Stronger security standard.
    
- Uses **AES-CCMP** encryption.
    

### **WPA3**

- Latest and most secure.
    
- Uses **SAE** for authentication (protects against offline cracking).
    
- Provides stronger enterprise-grade encryption.
    

---

# **5.3.5 Authenticating a Home User**

Home routers typically offer:

### **WPA2 Personal (PSK)**

- Most common for home Wi-Fi.
    
- Users authenticate with a **pre-shared password**.
    
- No RADIUS server required.
    

### **WPA2 Enterprise**

- Used in businesses.
    
- Requires:
    
    - **RADIUS server**
        
    - **802.1X** authentication
        
    - **EAP** methods for user identity verification
        

### **Key Difference**

- **Personal = shared password**
    
- **Enterprise = per-user authentication via RADIUS**
    

---

# **5.3.6 Encryption Methods**

Encryption protects wireless data from being read by attackers.

### **TKIP (WPA)**

- Patch to improve WEP.
    
- Encrypts Layer 2 payload using TKIP.
    
- Uses MIC (Message Integrity Check).
    
- Legacy, not secure today.
    

### **AES-CCMP (WPA2)**

- Strong, modern encryption standard.
    
- Provides integrity + confidentiality.
    
- Preferred for all modern Wi-Fi deployments.
    

---

# **5.3.7 Authentication in the Enterprise**

Enterprise Wi-Fi uses **WPA2-Enterprise or WPA3-Enterprise**, requiring:

### **AAA Components**

- **RADIUS server** (for authentication + accounting)
    
- **UDP ports**
    
    - 1812 → Authentication
        
    - 1813 → Accounting
        
    - (Old ports: 1645/1646)
        

### **Shared Secret Key**

- Configured **only** between AP and RADIUS server.
    
- Not used by clients.
    

### **User Authentication Process**

Uses the **802.1X framework**:

1. Client requests authentication.
    
2. AP relays credentials to RADIUS server.
    
3. RADIUS validates user using **EAP** (PEAP, EAP-TLS, etc.).
    
4. Secure session keys are generated for encryption.
    

---

# **5.3.8 WPA3**

WPA3 improves security significantly over WPA2 and introduces four modes:

### **1. WPA3-Personal**

- Uses **SAE (Simultaneous Authentication of Equals)**.
    
- Protects against offline dictionary attacks.
    
- PSK is never exposed.
    

### **2. WPA3-Enterprise**

- Still uses 802.1X/EAP.
    
- Requires **192-bit security suite**.
    
- Compliant with **CNSA** for high-security environments.
    

### **3. WPA3 for Open Networks**

- Public Wi-Fi uses **OWE (Opportunistic Wireless Encryption)**:
    
    - No authentication
        
    - But **all traffic is encrypted**
        

### **4. WPA3 IoT Onboarding**

- Designed to securely onboard IoT devices that lack screens/keyboards.
    

---


