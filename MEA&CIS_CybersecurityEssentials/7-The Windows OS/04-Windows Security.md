
---

# **7.4.1 The netstat Command**

The **netstat** command helps identify suspicious network connections opened by malware.

### **Purpose**

- Malware often opens unauthorized ports to send/receive data.
    
- `netstat` shows all active TCP connections.
    
- `netstat -abno` links connections to the **process names** and **PIDs**.
    

### **Useful Flags**

- **-a** → show all connections + listening ports
    
- **-b** → show executable that opened the port
    
- **-n** → show addresses in numeric format
    
- **-o** → show PID
    

### **Process**

1. Run Command Prompt as **Administrator**.
    
2. Use `netstat -abno` to list:
    
    - Local + foreign IPs
        
    - Connection state
        
    - Executable name
        
    - PID
        
3. Investigate suspicious processes.
    
4. Use PID to locate process in **Task Manager** (enable PID column).
    
5. Terminate malicious processes and use antivirus tools to remove malware.
    

---

# **7.4.2 Event Viewer**

Windows **Event Viewer** stores logs for system, security, and application activity.

### **Log Categories**

- **Windows Logs:** Application, Security, System, Setup
    
- **Application and Services Logs:** More specific event logging
    

### **Event Properties**

- Level (Information, Warning, Error, Critical)
    
- Date/time
    
- Source
    
- Event ID
    
- Description
    

### **Custom Views**

- Filter events by:
    
    - Time
        
    - Level
        
    - Source
        
    - Keywords
        
- **Administrative Events** → built-in view showing all critical/errors/warnings
    

### **Security Logs**

- Found under **Windows Logs → Security**
    
- Use Event IDs to identify authentication, access, and audit events
    

---

# **7.4.3 Windows Update Management**

Updates protect systems against new vulnerabilities and zero-day attacks.

### **Types of Updates**

- **Security updates**
    
- **Critical updates**
    
- **Service packs** (bundled updates)
    

### **Why Updates Matter**

- Fix vulnerabilities before or after exploitation
    
- Reduce impact of malware outbreaks
    
- Prevent attacks caused by outdated systems
    

### **Windows Update Features**

- Check for updates manually
    
- View update history
    
- Configure active hours (prevent automatic restart)
    
- Set restart options
    
- Advanced settings for update installation behavior
    

Enterprises often use centralized tools to automate patching.

---

# **7.4.4 Local Security Policy**

Defines local security rules for standalone Windows systems (not using AD Domain Policies).

### **Key Elements**

- **Password Policy**
    
    - Minimum length
        
    - Complexity
        
    - Expiration
        
- **Account Lockout Policy**
    
    - Number of failed login attempts
        
    - Lockout duration
        
- **User Rights Assignments**
    
- **Security Options**
    
- **AppLocker** rules (restrict which apps can run)
    
- **Local Firewall Rules**
    

### **Uses**

- Hardening standalone systems
    
- Ensuring consistent local security configurations
    
- Exporting/importing policies for multiple machines (`.inf` file)
    

### **Auto-Lock Rule**

- Require PC to lock when screensaver activates
    

---

# **7.4.5 Windows Defender**

Built-in antimalware system included in Windows.

### **Types of Malware It Detects**

- Viruses
    
- Worms
    
- Trojans
    
- Keyloggers
    
- Spyware
    
- Adware
    

### **Functions**

- Real-time protection
    
- Manual scans
    
- Quarantine and removal
    
- Anti-phishing checks
    
- App/browser protection
    
- Device performance monitoring
    

### **Important Tools in Defender**

- Virus & Threat Protection
    
- Firewall & Network Protection
    
- App & Browser Control
    
- Device Security
    
- Scan history
    
- Definition (signature) updates
    

Only run **one** real-time antimalware tool at a time.

---

# **7.4.6 Windows Defender Firewall**

Controls network traffic to/from the computer by managing allowed ports and applications.

### **Security Policy Types**

- **Restrictive policy** → block everything except what is allowed (recommended)
    
- **Permissive policy** → allow everything except blocked items (dangerous)
    

Modern systems default to being restrictive.

### **Key Features**

- Allow/block applications
    
- Enable/disable firewall
    
- Configure inbound/outbound rules
    
- Advanced settings:
    
    - Custom port rules
        
    - Protocol rules
        
    - Program-based rules
        
    - Profile selection (Domain, Private, Public)
        
    - Monitoring of active rules
        

### **If using a 3rd-party firewall**

- Windows Defender Firewall must be manually disabled.
    

---
