
---

# **11.1.1 Assets, Vulnerabilities, Threats**

- **Assets** → Anything valuable that must be protected (servers, endpoints, infrastructure, and especially **data**).
    
- **Vulnerabilities** → Weaknesses in systems or designs that can be exploited.
    
- **Threats** → Any potential danger to assets (attackers, malware, disasters, misuse).
    

---

# **11.1.2 Identify Assets**

Organizations grow fast → assets multiply (servers, endpoints, cloud services, mobile devices).  
All assets = **attack surface**.

**Asset management** includes:

- Inventorying all assets
    
- Identifying critical information
    
- Applying protection based on importance
    

Different businesses store different critical data (credit cards, designs, financial info), attracting different threat actors.

---

# **11.1.3 Avatar**

You advance to supporting asset & risk management.

---

# **11.1.4 Asset Classification**

Assets are grouped based on value, sensitivity, and criticality.

### **Steps**

1. **Identify asset categories**
    
    - Information
        
    - Software
        
    - Physical devices
        
    - Services
        
2. **Define ownership**
    
    - Who owns each information asset?
        
    - Who owns each software?
        
3. **Set classification criteria**
    
    - Confidentiality
        
    - Value
        
    - Time sensitivity
        
    - Access rights
        
    - When/how to destroy
        
4. **Apply a classification system**
    
    - Consistent labels → uniform protection & easier monitoring.
        

---

# **11.1.5 Asset Standardization**

Organizations should standardize hardware & software to:

- Reduce complexity
    
- Speed up replacement/repairs
    
- Lower costs of maintenance
    
- Simplify management
    

Non-standard setups = higher cost + more work.

---

# **11.1.6 Asset Lifecycle Stages**

1. **Procurement**  
    – Buying the asset based on business needs.
    
2. **Inventory**  
    – Adding it to the asset list.
    
3. **Testing & Tagging**  
    – Assembling, testing, labeling (barcodes, tags).
    
4. **Deployment**  
    – Asset enters active use.
    
5. **Utilization**  
    – Longest phase: upgrades, patches, audits, performance checks.
    
6. **Maintenance**  
    – Extending useful life, modifying components.
    
7. **Retirement & Disposal**  
    – Data wiping and safe disposal; environmental rules apply.
    

---

# **11.1.7 Your Turn (Correct Mapping)**

- Checking new laptops → **Inventory**
    
- Adding barcodes → **Testing & Tagging**
    
- Rolling out patches → **Utilization**
    
- Upgrading outdated assets → **Maintenance**
    
- Removing broken equipment → **Retirement/Disposal**
    

---

# **11.1.8 Identify Vulnerabilities**

Threat identification asks:

- What vulnerabilities exist?
    
- Who could exploit them?
    
- What happens if they succeed?
    

**Example: e-Banking threats**

- Internal compromise
    
- Stolen customer data
    
- Fraudulent transactions
    
- Insider attacks
    
- Input errors
    
- Data center destruction
    

This requires understanding all systems, apps, and hardware.

---

# **11.1.9 Identify Threats – Defense in Depth**

Multiple layers of security protect assets.

### Example Layers:

1. **Edge Router (R1)**  
    – First screen of inbound traffic.
    
2. **Firewall**  
    – Tracks state, enforces rules, blocks external initiation.
    
3. **Internal Router (R2)**  
    – Final filtering before traffic reaches internal systems.
    

Other layers can include IPS, AMP, email/web security, AAA, NAC, etc.

If one layer fails, others still protect the asset.

---

# **11.1.10 The Security Onion & The Security Artichoke**

### **Security Onion**

- Layers of protection around assets.
    
- Attacker must peel through each defense (firewall → IPS → AAA → hardened devices…).
    

### **Security Artichoke**

Modern networks give attackers shortcuts:

- Mobile devices, IoT, cloud → each is a “leaf.”
    
- Attackers can bypass some layers by compromising just one weak leaf.
    
- Not every leaf must be removed to reach the “heart” (critical data).
    

---

# **11.1.11 Defense in Depth Strategies**

A single layer of defense is **not enough**.  
Organizations should combine multiple strategies:

### **1. Layering**

Many distinct layers (physical security + passwords + firewalls + encryption).  
If one fails, others still protect.

### **2. Limiting**

Restrict access → users only get what they need.  
Done through file permissions, access control, locked rooms, procedures.

### **3. Diversity**

Different types of defenses:

- Different vendors
    
- Different authentication methods
    
- Different encryption types
    

Prevents attackers from using one method to compromise all layers.

### **4. Obscurity**

Hide system information:

- Avoid leaking OS versions, device types
    
- Error messages must reveal nothing to attackers
    

### **5. Simplicity**

- Internally → simple for employees to use correctly
    
- Externally → complex for attackers to break
    

Too much complexity can cause misconfigurations, which become vulnerabilities.

---

If you want, I can continue with **Module 11.2** — just say **continue**.