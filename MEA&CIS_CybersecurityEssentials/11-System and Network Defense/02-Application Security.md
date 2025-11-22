

---

# **12.2.2 Application Development**

Secure application development follows a structured process to ensure security at every stage:

- **Requirements** — define functional and security requirements.
    
- **Design** — plan secure architectures, data flows, and access controls.
    
- **Development** — implement secure coding, follow standards, perform code reviews.
    
- **Testing** — test for vulnerabilities, errors, and logic flaws.
    
- **Deployment** — ensure secure configuration, access control, and patch levels.
    
- **Maintenance** — apply updates, fix vulnerabilities, monitor logs.
    
- **Retirement** — securely remove or archive the application and its data.
    

---

# **12.2.3 Security Coding Techniques**

### **Normalization**

Converts input into a standard, simplified form so malicious variations cannot bypass validation.

### **Stored Procedures**

Precompiled SQL statements inside the database that reduce attack surface and improve speed.

### **Obfuscation & Camouflage**

Hide code or sensitive logic to prevent reverse engineering.

### **Code Reuse**

Using existing, tested components to speed development; must avoid importing old vulnerabilities.

### **Third-Party Libraries / SDKs**

Useful for rapid development but can introduce widespread vulnerabilities if outdated.

---

# **12.2.5 Input Validation**

Applications must verify and sanitize all user input.

Why?  
To stop malformed, malicious, or manipulated input from reaching the backend (e.g., SQL injection, URL tampering, logic manipulation).

Example:  
Attackers modify confirmation URLs in newsletters → database is filled with bogus subscribers → application corrupted.

---

# **12.2.6 Validation Rules**

Validation rules ensure accurate, complete, and consistent data:

- **Size** – character count
    
- **Format** – matches pattern
    
- **Consistency** – related fields match (e.g., country code + phone format)
    
- **Range** – numeric limits
    
- **Check Digit** – mathematical checksum to detect input errors (e.g., ISBN)
    

---

# **12.2.7 Integrity Checks**

### **Checksums**

Verify that data was not changed during storage or transfer.

Process:

1. Sender calculates checksum (hash).
    
2. Data + checksum sent.
    
3. Receiver recalculates checksum.
    
4. If identical → data is intact.
    

### **Hash Algorithms**

- MD5
    
- SHA-1
    
- SHA-256
    
- SHA-512
    

### **Version Control**

Prevents simultaneous edits and accidental modification.

### **Backups**

Protect data if corruption occurs.

### **Authorization**

Restricts who can read/modify data.

---

# **12.2.8 Other Application Security Practices**

### **Digital Signatures**

Verify that downloaded software is authentic and unmodified.

### **Certificates / HTTPS**

Ensure secure encrypted communication when browsing websites.

### **Cookies**

Store session data securely for browsing continuity.

### **Code Signing**

Confirms software has not been altered.

---

# **12.2.9 Over to You — Answers**

Here are the correct matches:

1. **Measures data consistency by taking a snapshot**  
    → _Checksum / Integrity Check_
    
2. **Stores data securely for future requests while browsing**  
    → _Cookie_
    
3. **Checks that data falls within predefined parameters**  
    → _Validation Rule_
    
4. **Digitally validates that software code has not changed**  
    → _Code Signing / Digital Signature_
    

---

# **12.2.10 Managing Threats to Applications — Countermeasures**

### **Physical Threats**

- Implement policies and procedures for staff and visitors.
    

### **Availability Threats**

- Business continuity plan
    
- Disaster recovery plan
    

### **Software Vulnerabilities**

- Update OS and applications
    
- Install patches regularly
    

### **Unauthorized Access**

- Multi-factor authentication
    
- Monitor logs
    

### **Data Loss or Exposure**

- Data classification
    
- Backup procedures
    

### **Software Quality Issues**

- Thorough software testing before launch
    

---

If you want, I can continue with **12.2.11 – OWASP summary** next.