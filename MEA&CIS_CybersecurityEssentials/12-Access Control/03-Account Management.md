
---

## **13.3.2 Account Types 

**Key points:**

- Never share **privileged, admin, or application accounts**.
    
- Admin account must only be used for admin tasks → using it for browsing/email = high risk.
    
- OS installs **default accounts** (guest, admin, etc.) → attackers know them.
    
- Replace or disable default accounts.
    
- Ensure **every account requires a strong password**.
    
- Good practices include:
    
    - Disable unused accounts.
        
    - Rename default admin accounts.
        
    - Force password policy for all account types.
        

---

## **13.3.4 File Access Control 

Permissions restrict folder/file access based on **least privilege** and **need-to-know**.

### **Permission Levels**

- **Full Control** → read, write, delete, modify, create, run programs.
    
- **Modify** → change/delete existing files, cannot create new ones.
    
- **Read & Execute** → view content + run programs.
    
- **Write** → create new files/folders + modify existing ones.
    
- **Read** → view folder contents and open files.
    

Limiting access = reduces impact if device is compromised.


---

## **13.3.7 Account Policies in Windows 

Windows domains use **Active Directory** to enforce policies automatically.

### **Local Security Policy (secpol.msc)** applies only to standalone PCs.

### **Password Policy example:**

- Change password every **90 days**.
    
- Password must be used ≥ **1 day**.
    
- Minimum **8 characters**, must include **3 of 4** categories.
    
- Cannot reuse a password until **24** unique passwords have been used.
    

### **Account Lockout Policy:**

- 5 failed attempts → lock for 30 minutes.
    
- After 30 minutes, counter resets.
    

### **Audit Policies track:**

- Logon events
    
- Account management
    
- Directory access
    
- Object access
    
- Policy changes
    
- Privilege use
    
- System events
    

---

## **13.3.8 Authentication Management 

How to secure sign-ins:

- **SSO** → one strong password for multiple applications.
    
- **OAuth** → login via Google/Facebook for third-party apps.
    
- **Password vault** → encrypts/stores all credentials.
    
- **KBA (Knowledge-Based Authentication)** → personal questions for password recovery.
    

---

## **13.3.10 HMAC 

HMAC = _Hash + secret key_ to authenticate messages.

- Prevents sending plaintext credentials.
    
- Server compares its HMAC with user’s HMAC → must match.
    
- Used in **IPsec**, VPNs, routing protocols.
    
- Provides:
    
    - Authentication
        
    - Integrity
        

---

## **13.3.12 Authentication Protocols & Technologies
### MS-CHAP

- Client sends password hash.
    
- Server uses certificate, client doesn’t.
    

### **PAP**

- Username/password sent **in plaintext**.
    
- Very insecure.
    

### **CHAP**

- Uses **one-way hash challenge**.
    
- Periodically re-authenticates during the session.
    
- Much more secure than PAP.
    

### **RADIUS**

- Used for **AAA** (authentication, authorization, accounting).
    
- Only encrypts **password**, everything else is cleartext.
    
- Uses **UDP**.
    
- Vulnerable unless protected against replay attacks.
    

### **TACACS+**

- Encrypts **all data** (username, password, accounting, permissions).
    
- Uses **TCP**.
    
- Better for enterprise networks needing fine-grained control.
    

### **Kerberos**

- Uses strong encryption + mutual auth.
    
- Uses **tickets**:
    
    - Ticket-granting ticket (TGT)
        
    - Service ticket
        
- Eliminates plaintext password transmission.
    
- Tickets expire → prevents replay attacks.
    

---

## **13.3.13 Hash Function Applications 

Used for:

- Authenticity (IPsec, routing protocol authentication).
    
- Challenge-response authentication.
    
- Digital signatures, integrity verification.
    
- PKI certificates.
    

Use **SHA-256+**.  
Avoid **MD5** and **SHA-1**.

---

## **13.3.15 Access Control Strategies 

### **Mandatory Access Control (MAC)**

- Uses **labels** and **clearances**.
    
- Users cannot change permissions.
    
- Used in government/military.
    

### **Discretionary Access Control (DAC)**

- Object owner decides permissions.
    
- Uses **ACLs**, read/write/execute settings.
    
- Flexible but less secure.
    

### **Role-Based Access Control (RBAC)**

- Access based on **job role**.
    
- Scales well for large organizations.
    
- Best practice for enterprise permissions.
    

### **Rule-Based Access Control**

- Access based on **rules**, e.g.:
    
    - “No access to payroll after 18:00.”
        
- Combined often with MAC/DAC.
    

---
