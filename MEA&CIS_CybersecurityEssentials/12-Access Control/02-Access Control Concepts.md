
---

## **13.2.1 Zero Trust Security**

Zero Trust = **“Never trust, always verify.”**  
Every access request is treated as untrusted until re-validated.

### **Key Points**

- Applies to **users, devices, APIs, IoT, containers, microservices**, etc.
    
- Prevents unauthorized access, limits lateral movement, and contains breaches.
    
- Unlike traditional perimeter security, **every access point becomes a perimeter**.
    
- Multiple authentications may be required at different layers.
    

### **3 Pillars of Zero Trust**

#### **1. Workforce**

- Employees, contractors, vendors using corporate or personal devices.
    
- Ensures **only verified users + secure devices** access applications.
    

#### **2. Workloads**

- Applications, containers, microservices, APIs, cloud workloads.
    
- Controls how app components securely access each other.
    

#### **3. Workplace**

- All devices connected to the enterprise network:  
    IoT, servers, cameras, HVAC, printers, industrial control systems, etc.
    
- Ensures secure access for **everything** connected to the network.
    

---

## **13.2.2 Access Control Models**

Different models define how access decisions are made.

### **1. DAC – Discretionary Access Control**

- **Least restrictive** model.
    
- Data owners decide who can access their resources.
    
- Often uses ACLs.
    

### **2. MAC – Mandatory Access Control**

- **Most restrictive**, used in military/government.
    
- Access based on **security clearances + data classification labels**.
    

### **3. RBAC – Role-Based Access Control**

- Access based on **roles** and job functions.
    
- Users inherit privileges of their assigned role.
    
- Also called **non-discretionary** access control.
    

### **4. ABAC – Attribute-Based Access Control**

- Access based on **attributes**:
    
    - Subject attributes (user)
        
    - Object attributes (resource)
        
    - Environment (time, location, device, etc.)
        

### **5. Rule-Based Access Control (Rule-Based RBAC)**

- Uses **administrative rules**, such as:
    
    - Allowed IPs
        
    - Allowed protocols
        
    - Time of day restrictions
        

### **6. TAC – Temporal Access Control**

- Access based on **time and date**.
    

### **Principle of Least Privilege**

- Users receive **only the access needed** for their tasks.
    
- Reduces attack surface and limits damage.
    

### **Privilege Escalation**

- Attackers exploit vulnerabilities to gain **higher privileges** than allowed.
    

---

## **13.2.3 Network Access Control (NAC)**

NAC systems enforce **who** and **what devices** can access the network.

### **Capabilities**

- Enforce access policies automatically.
    
- Identify, profile, and monitor all connected devices.
    
- Provide secure guest access via portals.
    
- Check device compliance (OS, patches, antivirus, configuration).
    
- Isolate or block non-compliant devices.
    
- Prevent malware-infected BYOD/IoT devices from joining the network.
    

### **Why NAC is essential**

- BYOD and IoT dramatically increase the attack surface.
    
- NAC provides automated enforcement → **scales to thousands of devices**.
    
- Integral to **Zero Trust Architecture** → verify every user and device before access.
