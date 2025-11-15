

---

# **1.4 Wireless and Mobile Device Attacks**

---

## **1.4.2 Grayware and SMiShing**

### **Grayware**

- Grayware refers to **unwanted or annoying applications** that, while not overtly malicious, still pose **security and privacy risks**.
    
- These apps may:
    
    - Track user location
        
    - Display intrusive ads
        
    - Collect data without proper consent
        
- Developers often include these invasive permissions in the **fine print** of license agreements.
    
- Grayware is a growing **mobile security concern**, as users frequently install apps without reviewing permissions.
    

### **SMiShing**

- **SMiShing** (SMS phishing) involves sending **fraudulent text messages** to trick users into:
    
    - Visiting **malicious websites**
        
    - Calling **fake phone numbers**
        
    - Downloading **malware** or sharing **personal data**
        
- Attackers often disguise these texts as coming from **banks, delivery services, or employers**.
    

---

## **1.4.3 Rogue Access Points (Rogue APs)**

- A **rogue access point** is an **unauthorized wireless access point** installed on a secure network.
    
- It may be set up by:
    
    - A **well-meaning employee** seeking better Wi-Fi, or
        
    - A **hacker** exploiting poor physical security.
        

### **Attack Scenarios**

- **Social Engineering:**  
    Hackers gain physical access and secretly install a rogue AP.
    
- **Evil Twin:**  
    The attacker creates a **fake Wi-Fi network** with a similar name (SSID) but stronger signal, tricking users into connecting.
    
    - Once connected, all traffic can be **intercepted or modified**.
        

---

## **1.4.4 Radio Frequency (RF) Jamming**

- Wireless signals are vulnerable to:
    
    - **Electromagnetic interference (EMI)**
        
    - **Radio frequency interference (RFI)**
        
    - **Environmental noise** (e.g., lightning or fluorescent lights)
        
- **RF jamming** occurs when attackers **intentionally transmit interference** on the same frequency as a target signal, disrupting communication.
    

### **Successful Jamming Requires**

- Matching:
    
    - The **frequency**
        
    - **Modulation**
        
    - **Power output**  
        of the targeted wireless signal.
        

---

## **1.4.5 Bluetooth Exploitation**

- **Bluetooth** is a **low-power, short-range protocol** used to connect devices (phones, laptops, printers, etc.) via pairing.
    
- Attackers exploit Bluetooth vulnerabilities to access or control nearby devices.
    

---

## **1.4.6 Bluejacking and Bluesnarfing**

### **Bluejacking**

- **Non-destructive attack** where a hacker sends **unsolicited messages** (contacts, notes, or text) via Bluetooth.
    
- Purpose: usually **annoying or prank-based**, but can be a **gateway** to other attacks.
    

### **Bluesnarfing**

- **Serious Bluetooth attack** where the attacker:
    
    - **Steals data** (contacts, messages, files)
        
    - Gains **unauthorized access** to the target device
        
- Requires the attacker to be **within Bluetooth range**.
    

---

## **1.4.7 Wi-Fi Protocol Attacks**

### **WEP (Wired Equivalent Privacy)**

- Designed to provide encryption similar to wired networks.
    
- Vulnerabilities:
    
    - **Weak key management**
        
    - **Static and small initialization vector (IV)**
        
    - Easily cracked using packet sniffers
        
- Result: **Obsolete and insecure**.
    

### **WPA and WPA2 (Wi-Fi Protected Access)**

- Developed to **replace WEP** and fix its flaws.
    
- **WPA2** uses stronger encryption (AES) and dynamic key exchange.
    
- While more secure, attackers can still **capture and analyze packets** to attempt brute-force or dictionary attacks.
    

---

## **1.4.8 The Risky Business Scenario**

**Scenario:**  
You’re at a café and connect to what seems like the public Wi-Fi.  
The signal is strong, but it’s actually a **fake network created by a nearby hacker**.

**Answer:** 🟩 **Evil Twin Attack**

> The hacker’s fake access point mimics a legitimate Wi-Fi network to intercept data and monitor users’ online activity.

---

## **1.4.9 Wi-Fi and Mobile Defense**

### **Defensive Measures**

1. **Change Default Configurations**
    
    - Modify default Wi-Fi SSIDs, passwords, and encryption settings.
        
    - Always enable **authentication and encryption**.
        
2. **Access Point Placement**
    
    - Place APs **outside the internal firewall** or in a **DMZ** (demilitarized zone).
        
    - Prevents direct access to the internal LAN.
        
3. **Monitor Wireless Networks**
    
    - Use tools like **NetStumbler** or other **WLAN scanners** to detect rogue APs.
        
4. **Guest Network Policies**
    
    - Create **separate VLANs or SSIDs** for guest Wi-Fi access.
        
5. **Use VPNs**
    
    - Employees should use a **secure VPN** for all wireless connections to protect data in transit.
        

---

Would you like me to continue with **Section 1.5 – Network Attacks and Defenses** next, keeping the same clean, structured Obsidian layout?