
---

# **4.2 – Web, Email, and Application Attacks**

---

## **4.2.1 – HTTP and HTTPS**

### **How typical web-based attacks work**

1. Victim visits a compromised web page.
    
2. Page silently redirects through multiple infected servers.
    
3. Victim lands on a malicious site → **drive-by download**.
    
4. Exploit kit scans the victim’s software (OS, Java, Flash, browser).
    
5. Exploit kit downloads code exploiting the detected vulnerability.
    
6. Victim’s machine downloads and runs the malware payload.
    

### **Attack goal**

Make the victim’s browser eventually reach the attacker’s website containing the exploit.

### **HTTP Status Codes**

- **1xx – Informational**
    
- **2xx – Success**
    
- **3xx – Redirection**
    
- **4xx – Client error**
    
- **5xx – Server error**
    

### **Defenses**

- Keep OS & browsers fully patched.
    
- Use web proxies (Cisco CWS, WSA).
    
- Follow **OWASP Top 10** for secure development.
    
- Educate users about risky websites.
    

---

## **4.2.2 – Common HTTP Exploits**

### **1. Malicious iFrames**

- Hidden iFrames (sometimes 1–5 pixels)
    
- Load external malicious pages
    
- Used for:
    
    - Spam
        
    - Exploit kits
        
    - Malware delivery
        

**Mitigation:**  
– Block malicious sites (proxy, Cisco Umbrella)  
– Avoid using iFrames in web apps  
– Train users

---

### **2. HTTP 302 Cushioning**

- Attacker abuses **HTTP 302 redirects**.
    
- Browser is redirected through multiple malicious sites.
    
- Final destination: exploit kit landing page or malware site.
    

**Mitigation:**  
– Web proxy  
– Cisco Umbrella  
– Teach users how redirects work

---

### **3. Domain Shadowing**

- Attacker steals domain owner credentials.
    
- Creates multiple hidden subdomains.
    
- Used with:
    
    - 302 redirects
        
    - malicious infrastructure
        
    - exploit kits
        

**Mitigation:**  
– Strong passwords + MFA for domain accounts  
– Web proxies / Cisco Umbrella  
– Monitor for unauthorized subdomains

---

## **4.2.3 – Email Threats**

Email is the **#1 infection vector** today.

### **Common Email Attacks**

#### **1. Malicious Attachments**

- Malware hidden inside:
    
    - PDFs
        
    - Office documents
        
    - HTML emails
        

#### **2. Email Spoofing / Phishing**

- Forged sender address
    
- Victim tricked into giving:
    
    - credentials
        
    - financial info
        

#### **3. Spam**

- Bulk unsolicited email
    
- Often contains:
    
    - malicious links
        
    - malware
        
    - social engineering traps
        

#### **4. Open Mail Relay Abuse**

- Misconfigured SMTP server
    
- Anyone can send email through it → used by spammers
    

#### **5. Homoglyph Attacks**

- Characters that look similar:
    
    - O vs 0
        
    - l vs 1
        
- Used to hide malicious URLs
    

#### **6. Vulnerable SMTP Services**

- Outdated mail servers can be exploited
    

### **Mitigation**

- Keep mail servers updated
    
- Never run an open relay
    
- Use email security appliances (Cisco ESA)
    
- Educate users
    
- Teach them to verify links, attachments, and sender identity
    

---

## **4.2.4 – Web-Exposed Databases**

Web apps often connect to databases → huge attack surface.

### **1. Command Injection**

- Attacker injects OS commands via a web form
    
- Caused by missing **input validation**
    

### **2. SQL Injection**

- Attacker injects SQL commands into input fields
    
- Can:
    
    - read sensitive data
        
    - modify tables
        
    - escalate privileges
        
    - run OS commands (in some DBs)
        

### **Mitigation**

- Strong input validation
    
- Use prepared statements
    
- Sanitize all user input
    
- Monitor database logs for abnormal queries
    

---

## **4.2.5 – Client-Side Scripting (XSS)**

Cross-Site Scripting happens in the victim’s browser.

### **Two types of XSS**

#### **1. Stored (Persistent)**

- Malicious script **stored on server**
    
- Every visitor gets infected
    

#### **2. Reflected (Non-Persistent)**

- Script in a link
    
- User must click the link
    

### **Capabilities of XSS**

- Steal cookies & sessions
    
- Steal credentials
    
- Spread malware
    
- Redirect to malicious sites
    

### **Mitigation**

- Input validation (server-side + client-side)
    
- Use IPS/IDS
    
- Web proxies / Cisco Umbrella
    
- Educate users about suspicious links
    

---
