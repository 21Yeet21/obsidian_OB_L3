
---

# **5.1.2 Wireless vs. Wired LANs — Summary**

Wireless LANs (WLANs) operate very differently from wired LANs:

### **• Medium**

- **Wired LANs:** Use cables (Ethernet). Collision detection is possible (CSMA/CD).
    
- **Wireless LANs:** Use radio waves. Cannot detect collisions because devices cannot listen while transmitting.
    

### **• Half-Duplex**

- WLANs are **half-duplex** — only one device transmits at a time.
    
- Wired Ethernet (switch-based) is **full-duplex**.
    

### **• Interference**

- WLANs suffer from:
    
    - Other wireless devices
        
    - Walls, distance, and obstacles
        
    - Overlapping channels
        

### **• Security**

- Wired networks rely on physical security.
    
- WLANs broadcast signals through the air → require strong encryption and configuration.
    

### **• Coverage**

- Wireless coverage is based on radio signal strength.
    
- Wired coverage depends on cable length and network design.
    

---

# **5.1.3 802.11 Frame Structure — Summary**

The 802.11 wireless frame is similar to Ethernet but contains **more fields** due to mobility, association, and radio communication.

### **Frame Sections**

1. **Header**
    
2. **Payload (data)**
    
3. **Frame Check Sequence (FCS)**
    ![[Pasted image 20251113190025.png]]

### **Important Header Fields**

- **Frame Control**  
    Identifies frame type (management, control, data), power management, security, protocol.
    
- **Duration**  
    Indicates how long the channel must remain reserved.
    
- **Address 1**  
    Usually the receiver’s MAC (AP or client).
    
- **Address 2**  
    Sender’s MAC.
    
- **Address 3**  
    Often the destination (e.g., default gateway MAC).
    
- **Sequence Control**  
    Reassembly and sequencing of frames.
    
- **Address 4**  
    Only used in ad hoc mode (rare).
    

### **Payload**

Contains the actual data being transmitted.

### **FCS**

Used for Layer 2 error checking.

---

# **5.1.4 CSMA/CA — Summary**

Wireless networks use **CSMA/CA (Collision Avoidance)** instead of Ethernet’s CSMA/CD (Collision Detection).

Because WLAN clients cannot detect collisions while transmitting, they use:

### **Process**

1. **Listen** to check if the channel is free.
    
2. **Send RTS** (Request to Send).
    
3. AP replies with **CTS** (Clear to Send).
    
4. Client transmits data.
    
5. Client waits for **ACK** from AP.
    
6. If no ACK → assumes collision → retries after a random backoff time.
    

### **Key Point**

CSMA/CA prevents collisions _before_ they happen instead of detecting them after.

---

# **5.1.5 Wireless Client & AP Association — Summary**

A wireless device must complete **three stages** to connect:

### **1. Discover AP**

- Via beacon frames (passive)
    
- Or probe requests (active)
    

### **2. Authenticate**

- Open authentication (default)
    
- Or secure authentication (WPA2, etc.)
    

### **3. Associate**

- Client joins the AP’s network and receives parameters.
    

### **Necessary Matching Parameters**

- **SSID** (network name)
    
- **Password** (if protected)
    
- **Network mode** (802.11a/b/g/n/ac/ax)
    
- **Security mode** (WPA2, WPA3, etc.)
    
- **Channel** (auto or manually configured)
    

---

# **5.1.6 Passive & Active Discovery Modes — Summary**

Wireless clients discover APs using **passive** or **active** methods.

---

## **Passive Mode**

- AP sends **beacon frames** periodically.
    
- Beacon contains:
    
    - SSID
        
    - Supported standards
        
    - Security settings
        
- Client listens and detects available networks.
    
- Required when SSID is broadcast.
    

---

## **Active Mode**

- Client sends **probe request**:
    
    - With SSID (specific Wi-Fi)
        
    - Or without SSID (search for any open AP)
        
- AP replies with a **probe response** containing:
    
    - SSID
        
    - Supported standards
        
    - Security settings
        
- Needed when AP **does not broadcast** the SSID.
    

---

