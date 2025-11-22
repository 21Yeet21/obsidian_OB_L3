
---

# **12.3.2 Network and Routing Services**

Cybercriminals target weak or exposed network services. A port scanner checks which services are open by probing ports — the same technique attackers use. Only necessary ports should be open.

### **DHCP**

Assigns IP addressing info to devices. Attackers may deploy rogue DHCP servers to redirect traffic.  
**Security:**

- Physically secure DHCP server
    
- Patch regularly
    
- Place behind firewall
    
- Monitor logs
    
- Use DHCP snooping
    
- Remove unused services
    
- Close unused ports
    

### **DNS**

Resolves domain names to IP addresses. Attackers perform DNS poisoning, hijacking, or DoS.  
**Security:**

- Keep DNS updated
    
- Hide version info
    
- Separate internal/external DNS
    
- Restrict transactions by IP
    
- Use DNSSEC + signatures
    
- Restrict zone transfers
    
- Enable & review logs
    

### **ICMP**

Used for testing reachability (ping). Attackers use it for reconnaissance, DoS, covert channels.  
**Security:** Filter ICMP where possible.

### **RIP (Routing Information Protocol)**

Uses hop count (max 15). Attackers can alter routing updates to redirect or disrupt traffic.  
**Security:** Authentication for routing, patches, updates.

### **NTP (Network Time Protocol)**

Synchronizes device clocks — critical for logs and certificates.  
Attackers may alter time to hide traces.  
**Security:** Use NTP authentication to ensure trusted servers.

---

# **12.3.3 Telnet, SSH, and SCP**

### **Telnet**

- Uses plaintext login
    
- Captured easily in Wireshark
    
- Runs on TCP 23  
    **Not secure**
    

### **SSH (Secure Shell)**

- Encrypted remote access
    
- Protects credentials and data
    
- Runs on TCP 22  
    **Preferred over Telnet**
    

### **SCP (Secure Copy Protocol)**

- Secure file transfer
    
- Uses SSH for confidentiality + authentication
    

Attack example:

- Telnet session is sniffed → attacker obtains username/password.
    
- SSH session is sniffed → attacker sees only encrypted traffic.
    

---

# **12.3.4 Secure Protocols**

Cybersecurity professionals must replace legacy protocols with secure versions.

### **SNMP → SNMPv3**

- SNMPv3 uses authentication + encryption
    
- Protects device monitoring traffic
    

### **HTTP → HTTPS**

- HTTP (port 80) is unencrypted
    
- HTTPS uses SSL/TLS to encrypt traffic
    
- Users see **https://** in browser
    

### **FTP → FTPS**

- FTP sends credentials in plaintext
    
- FTPS adds SSL/TLS for encryption, integrity, and protection from tampering
    

### **Email Protocol Security**

Email uses:

- **POP**
    
- **IMAP**
    
- **MIME** (attachments)
    

Secure versions add TLS/SSL, such as:

- **POP3S**
    
- **IMAPS**
    
- **SMTP over TLS**
    

These protect email contents and credentials from interception.

---

If you want, I can also summarize **the rest of Module 12.3 or move to 12.4** — just tell me.