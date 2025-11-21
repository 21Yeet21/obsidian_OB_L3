
---

# **9.1.1 Operating System Security – Summary**

The operating system is a major target for attackers. Securing it is a primary responsibility for cybersecurity professionals.

Key points:

- The OS must be hardened to reduce vulnerabilities.
    
- Security controls protect the OS from malware, exploitation, and unauthorized access.
    
- Hardening includes disabling unnecessary services, installing updates, and reducing the attack surface.
    

---

# **9.1.2 Operating System Security (Details)**

To properly secure an OS, an organization must:

### **1. Have a good administrator**

- Removes unnecessary software/services.
    
- Installs patches quickly.
    
- Configures security settings to reduce risk.
    

### **2. Use a systematic update approach**

- Monitor security bulletins.
    
- Evaluate updates.
    
- Plan installation.
    
- Deploy patches following documented procedures.
    

### **3. Establish a baseline**

- A baseline is a reference of normal system performance and configuration.
    
- Used to detect anomalies or deviations caused by attacks or misconfigurations.
    

---

# **9.1.3 Types of Antimalware Programs**

Matches based on descriptions:

- **Looks for programs showing unwanted ads → Adware scanner**
    
- **Warns about unsafe programs/websites → Application control / Browser protection**
    
- **Blocks phishing IPs & warns about suspicious emails → Anti-phishing / Web protection**
    
- **Monitors for viruses & quarantines them → Antivirus**
    
- **Scans for keyloggers & spyware → Anti-spyware**
    

---

# **9.1.4 Important Antimalware Concepts**

### **Rogue Antivirus**

Fake antivirus popups that install malware when clicked.

### **Fileless Malware**

Lives in memory, uses legitimate tools (PowerShell), leaves no files to scan.

### **Malicious Scripts**

Scripts (Python, Bash, VBA) can embed malware logic.

### **Unapproved Software**

Non-compliant software may cause vulnerabilities and must be removed.

---

# **9.1.5 Patch Management – Summary**

### **What are patches?**

- Code updates that fix vulnerabilities.
    
- Often combined into service packs.
    
- Systems like Windows automatically check for critical updates.
    

### **Best practices**

- Test patches before deploying organization-wide.
    
- Use patch management tools for centralized control.
    

### **Benefits**

- Admins can approve/deny updates.
    
- Control installation timing.
    
- Generate update status reports.
    
- Prevent users from bypassing updates.
    

### **Proactive strategy**

Update both OS and third-party applications to reduce exploitation risks.

---

# **9.1.6 Endpoint Security – Summary**

Host-based security tools installed directly on a device protect it from threats. Examples:

- **Host-based firewalls**
    
- **HIDS/HIPS**
    
- **EDR**
    
- **DLP**
    
- **NGFW (when used on endpoints)**
    
![[Pasted image 20251121174839.png]]
These tools work with the OS to enforce local protection.

---

# **9.1.7 Encryption**

Encryption transforms readable data into unreadable text using an algorithm and a decryption key.

---

# **9.1.8 Host Encryption (Windows EFS & BitLocker)**

### **EFS**

Encrypts files/folders individually.

### **BitLocker (Full Disk Encryption)**

- Encrypts the entire drive.
    
- Requires **TPM** enabled in BIOS to securely store keys.
    

### **BitLocker To Go**

Encrypts removable USB drives without TPM.

### **Self-Encrypting Drives (SED)**

Hardware-based encryption built directly into the drive.

---

# **9.1.9 Boot Integrity**

### **Boot Integrity**

Ensures the system has not been tampered with during startup.

### **Secure Boot**

- Firmware validates signatures of all boot software.
    
- Only trusted code is allowed to load.
    

### **Measured Boot**

- Records measurements of each boot component into the TPM.
    
- Creates a log for remote verification.
    
- Detects untrusted changes earlier than Secure Boot.
    

---

# **9.1.10 Apple System Security Features**

Apple devices include:

- **Secure Enclave**: Hardware-based security CPU with dedicated AES engine.
    
- **FileVault**: Full-disk encryption using hardware-based AES.
    
- **Boot ROM**: Ensures macOS is genuine and untampered.
    
- **Biometric data isolation**: Touch ID/Face ID stored securely in hardware.
    
- **Find My Mac**: Locate, lock, or wipe a lost device.
    
- **XProtect**: Malware signature-based detection.
    
- **MRT**: Automatically removes detected malware.
    
- **Gatekeeper**: Allows only Apple-notarized apps to install.
    

---

# **9.1.11 Managing Device Threats**

Correct countermeasures:

- **Unpatched software → Apply updates/patches**
    
- **User downloads → Application allow-listing / restricting installs**
    
- **Malware → Antivirus/EDR**
    
- **Unattended devices → Auto-lock / screen lock**
    
- **Acceptable use violation → Enforce AUP policy**
    
- **Unauthorized media → USB port control / DLP**
    

---

# **9.1.12 Physical Protection of Devices**

### **Physical protections include:**

- **Cable locks** for laptops and desktops.
    
- **Locked telecom/server rooms**.
    
- **Faraday cages** to block electromagnetic signals.
    

### **Door Lock Types**

- **Keyed locks (weak)**
    
- **Deadbolt (stronger)**
    
- **Cipher lock**: Uses keycodes; can log entries.
    

### **RFID Systems**

- Track and secure assets.
    
- Control access (lock/unlock) using RFID cards or tags.
    

---

If you want, I can continue immediately with **Module 9.2 or 9.3**.