
---

# **1.3 Malware, Threats, and Attacks**

---

## **1.3.1 What’s the Difference?**

Cybercriminals use many types of **malicious software (malware)** to carry out attacks.  
Malware is code designed to:

- Steal data
    
- Bypass access controls
    
- Damage or compromise systems
    

---

## **1.3.2 Logic Bombs**

- A **logic bomb** is malware that stays dormant until a **specific trigger** occurs (e.g., a date, event, or database entry).
    
- Once activated, it can:
    
    - Corrupt or delete data
        
    - Attack applications or OS files
        
    - Even damage **hardware components** (CPU, fans, disks) by overloading them.
        

---

## **1.3.3 Ransomware**

- **Ransomware** locks systems or encrypts files until a ransom is paid.
    
- Victims are told that after payment, they’ll receive a **decryption key** — but often, access is **never restored**.
    
- Ransomware spreads via:
    
    - **Phishing emails** with malicious attachments
        
    - **Software vulnerabilities** or unpatched systems
        

---

## **1.3.4 Denial of Service (DoS) Attacks**

- A **DoS attack** floods a system or network with excessive traffic, causing:
    
    - Service downtime
        
    - Financial loss
        
    - Operational disruptions (even in industrial systems like utilities or factories)
        
- Simple to execute — even by unskilled attackers.
    

---

## **1.3.5 Distributed Denial of Service (DDoS)**

- A **DDoS attack** is a coordinated DoS attack using multiple compromised devices (a **botnet**).  
    **Steps:**
    
    1. Attacker builds a botnet of “zombie” computers.
        
    2. Zombies infect others, expanding the network.
        
    3. All zombies launch a massive coordinated DoS attack.
        

---

## **1.3.6 Domain Name System (DNS) Attacks**

### **DNS Basics**

- DNS translates domain names (e.g., `www.cisco.com`) into IP addresses.
    
- If DNS servers are compromised, attackers can redirect users to **malicious sites**.
    

### **Types of DNS Attacks**

- **DNS Spoofing / Cache Poisoning:**  
    Inserting false data into the DNS cache to redirect traffic to an attacker’s server.
    
- **Domain Hijacking:**  
    Unauthorized modification of DNS records — often via **email compromise** or **social engineering** targeting the WHOIS admin contact.
    
- **URL Redirection Exploits:**  
    Attackers modify legitimate redirects (e.g., login portals) to send users to fake or infected pages.
    

**Mitigation:**  
Monitor your domain’s **reputation** and ensure DNS configurations are secure.

---

## **1.3.7 Layer 2 Attacks**

Layer 2 = **Data Link Layer** in the OSI model.  
It handles data movement across physical links using **MAC addresses** and **ARP (Address Resolution Protocol)**.

### **Common Layer 2 Attacks**

#### **Spoofing (Impersonation)**

- **MAC Spoofing:** Attacker disguises their device as a trusted one.
    
- **ARP Spoofing:** Fakes ARP messages to associate the attacker’s MAC with another IP.
    
- **IP Spoofing:** Sends packets with fake source IPs to hide identity or impersonate others.
    

#### **MAC Flooding**

- The attacker floods a switch with fake MAC addresses.
    
- This **overloads** the switch’s memory, forcing it to broadcast traffic — exposing data to interception.
    

---

## **1.3.8 Identify the Attack**

@Apollo employees report:

- Slow PCs
    
- Pop-up ads
    
- Abnormal network traffic
    

➡️ **Most likely attack:**  
🟩 **Layer 2 Attack** (specifically ARP or MAC spoofing/flooding).

---

## **1.3.9 Man-in-the-Middle (MitM) and Man-in-the-Mobile Attacks**

- Attackers intercept or modify communications between two devices to:
    
    - Steal information
        
    - Impersonate one of the devices
        

### **Replay Attack Example**

- The hacker **captures communication** between two hosts and **replays** it to trick one party into acting — bypassing authentication mechanisms.
    

---

## **1.3.11 Zero-Day Attacks**

- A **Zero-Day Attack** exploits software vulnerabilities before the vendor releases a fix.
    
- “Day Zero” = the day the exploit becomes known but remains unpatched.
    
- Systems are most vulnerable between discovery and patch release.
    

**Defense Strategy:**  
Use **continuous monitoring**, **threat intelligence**, and **multi-layered defense architectures**.

---

## **1.3.12 Keylogging**

- **Keylogging** records every keystroke on a computer.
    
- Captures:
    
    - Usernames
        
    - Passwords
        
    - Visited sites
        
    - Personal data
        

### **Types:**

- **Software keyloggers** (installed secretly)
    
- **Hardware keyloggers** (plugged between keyboard and PC)
    

**Protection:**  
Anti-spyware tools can detect and remove unauthorized keyloggers.

> ⚠️ Note: Some keyloggers are **legitimate**, used by parents or employers for monitoring.

---

## **1.3.14 Confirm Your Details (Phishing Example)**

**Scenario:**  
An email from “HR” asks you to update your bank details by clicking a link.  
The sender’s email domain looks slightly altered.

➡️ **Answer:** 🟩 **Spoofing / Impersonation Attack**

---

## **1.3.15 Defending Against Attacks**

**Best Practices:**

1. Configure **firewalls** to block packets that pretend to originate internally.
    
2. Keep **patches and updates** current.
    
3. Use **load balancing** to reduce the impact of DoS attacks.
    
4. Block unnecessary **ICMP traffic** to prevent DoS and DDoS abuse.
    
5. Monitor network traffic continuously for **anomalies**.
    

---

Would you like me to continue with **Section 1.4 – Wireless and Mobile Device Attacks** next (in the same clean Obsidian structure)?