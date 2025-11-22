
---

## **13.4.1 AAA Operation **

AAA = framework that controls:

- **Who** can access the network (Authentication)
    
- **What** they can do (Authorization)
    
- **What** they did (Accounting)
    

### **1. Authentication – “Who are you?”**

- Verifies identity using:
    
    - username/password
        
    - tokens
        
    - challenge-response
        
    - smart cards
        
    - biometrics
        
- Centralized system ⇒ consistent access control.
    

### **2. Authorization – “What are you allowed to do?”**

- Defines permissions, allowed commands, allowed services.
    
- Example:  
    _User "student" can access server XYZ via SSH only._
    

### **3. Accounting – “What did you do?”**

- Logs user activity:
    
    - logon/logoff times
        
    - commands executed
        
    - bytes transferred
        
    - resources accessed
        
- Used for:
    
    - auditing
        
    - compliance
        
    - investigations
        

**Analogy:**  
Like a credit card:

- Authentication → Who uses the card
    
- Authorization → Spending limit
    
- Accounting → Transaction history
    

---

## **13.4.2 AAA Authentication 

AAA authentication is used for:

- **Administrative access**
    
- **Remote network access**
    

Cisco supports two models:

---

### **✔ Local AAA Authentication (small networks)**

Stored locally on the router.

**Process:**

1. User connects to router.
    
2. Router asks for username/password.
    
3. Credentials checked **locally**.
    

**Pros:**

- Simple
    
- No external server needed  
    **Cons:**
    
- Not scalable
    
- Must manually update each device
    

---

### **✔ Server-Based AAA Authentication (medium/large networks)**

Credentials stored on a **central AAA server** (RADIUS / TACACS+).

**Process:**

1. User connects to router.
    
2. Router requests username/password.
    
3. Router forwards this to AAA server.
    
4. Server accepts/denies and sends access profile.
    

**Pros:**

- Scalable
    
- Centralized management
    
- Stronger security options  
    **Cons:**
    
- Requires AAA server
    

---

## **13.4.3 AAA Accounting Logs**

Centralized AAA allows detailed logging across all devices.

### **Accounting logs include:**

- Start/stop connection times
    
- Commands executed
    
- Bytes/packets used
    
- System events
    
- Login failures/successes
    

### **How AAA Accounting works:**

1. After authentication → **Start accounting record** is created.
    
2. After session ends → **Stop record** created.
    

Used for:

- Troubleshooting
    
- Security audits
    
- Forensics
    

---

### **Types of AAA Accounting**

#### **1. Network Accounting**

- Tracks PPP sessions
    
- Packet/byte counts
    

#### **2. Connection Accounting**

- Tracks outbound connections (SSH, etc.)
    

#### **3. EXEC Accounting**

- Tracks user shell/terminal sessions
    
- Includes username, start/stop time, IP
    

#### **4. System Accounting**

- Tracks system events (reboot, config changes)
    

#### **5. Command Accounting**

- Logs **each command** executed
    
- Shows username + timestamp
    

**Cisco AAA also logs failed authentication attempts → important for security monitoring.**

---
![[Pasted image 20251122143025.png]]