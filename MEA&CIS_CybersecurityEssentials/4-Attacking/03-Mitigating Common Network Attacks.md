
---

# **4.3.5 Mitigating Access Attacks — Summary**

Access attacks commonly succeed due to weak passwords, excessive trust relationships, lack of encryption, or social engineering. Several defenses are used to reduce these risks:

### **• Strong Password Security**

- Use strong passwords (minimum 8 characters, mix of upper/lowercase, numbers, symbols).
    
- Lock or disable accounts after a certain number of failed login attempts.
    
- This helps stop brute-force and password-guessing attacks.
    

### **• Principle of Minimum Trust**

- Devices and systems should only trust each other when absolutely necessary.
    
- Example: a trusted internal server should not automatically trust web servers accessible to untrusted users.
    

### **• Cryptography**

- Encrypt remote access sessions (SSH, VPN, TLS).
    
- Encrypt routing protocol traffic when possible.
    
- Use encrypted or hashed authentication protocols.
    
- Encryption reduces opportunities for man-in-the-middle attacks.
    

### **• User Awareness + Multifactor Authentication**

- Educate employees about social engineering, phishing, and identity confirmation.
    
- MFA adds strong protection by requiring something beyond a password (token, SMS code, authenticator app, etc.).
    

### **• Detecting Access Attacks**

- Review logs for unusual login attempts.
    
- Monitor bandwidth and system load for suspicious behavior.
    
- Maintain logs for all network devices according to network security policy.
    

---

# **4.3.6 Mitigating DoS Attacks — Summary**

DoS attacks aim to overwhelm systems or networks, making services unavailable. Early indicators include slow response times, service outages, or user complaints.

### **• Detecting DoS Activity**

- Monitor network utilization graphs to identify unusual spikes.
    
- Use network behavior analysis tools to detect abnormal traffic patterns.
    
- Organizations should require continuous monitoring as part of their security policy.
    

### **• Impact of DoS Attacks**

- Devices like routers and firewalls may exceed their packet-per-second limits.
    
- Can cause outages for both the victim and network infrastructure along the path.
    
- Large-scale attacks may affect entire regions of the internet.
    

### **• Mitigation Techniques**

Cisco devices include many antispoofing technologies to reduce the impact of DoS attacks:

- **Port Security** – limits the number of allowed MAC addresses on a port.
    
- **DHCP Snooping** – blocks rogue DHCP servers.
    
- **IP Source Guard** – prevents IP spoofing by binding IP–MAC–port.
    
- **Dynamic ARP Inspection (DAI)** – blocks ARP spoofing attempts.
    
- **ACLs** – filter unwanted or spoofed traffic.
    

These techniques help prevent the spoofing commonly used in DoS and DDoS attacks.

---

