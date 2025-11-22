

---

## **12.5 Wireless Device Security – Summary**

### **Wireless Security Evolution**

- **WEP** – very weak, easily cracked.
    
- **WPA** – improves security with **MIC** (Message Integrity Check) and **TKIP**.
    
- **WPA2** – mandatory **AES/CCMP**, far stronger.
    
- **WPA3** – strengthens cryptography and key exchange.
    
- **WPS** – insecure; attackers can brute-force the PIN.
    

---

## **12.5.5 Authentication Basics**

Wireless devices are vulnerable to:

- Theft
    
- Sniffing
    
- MITM attacks
    
- Unauthorized remote access
    
- Performance/DoS attacks
    

**Best protection:**

- Strong authentication
    
- Encryption (WPA2/WPA3)
    

---

## **12.5.6 EAP Authentication Protocols**

EAP is a framework that uses an access point and an authentication server.

Comparison:

|Protocol|Client Cert|Server Cert|Deployment|Security|
|---|---|---|---|---|
|**EAP-TLS**|Yes|Yes|Difficult|High|
|**EAP-TTLS**|No|Yes|Moderate|Medium|
|**PEAP**|No|Yes|Moderate|Medium|
|**EAP-FAST**|No|No|Easy|Medium|

---

## **12.5.8 Mutual Authentication**

A rogue access point can imitate your legitimate AP → leads to MITM attacks.

**Mutual authentication ensures:**

- The **client** verifies the AP.
    
- The **AP** verifies the client.  
    This prevents connecting to rogue access points.
    

---

## **12.5.10 Mobile Communication Methods**



1. **Wi-Fi / Bluetooth**  
    → Wireless communication between devices.
    
2. **NFC / Contactless Payment**  
    → Short-range communication for payments (cards/phones).
    
3. **Screen Casting / Wireless Display**  
    → Phone sends video/audio to TV via Wi-Fi Direct / Miracast.
    
4. **USB Cable Connection**  
    → Physical tethering, charging, and data transfer.
    

---

## **12.5.11 Mobile Device Management (MDM)**

**Containerization**

- Splits device into **work** and **personal** areas.
    
- Allows remote wipe of **only** corporate data.
    

**Content Management**  
Controls data shared via cloud storage apps (Google Drive, Dropbox, etc.)

**Application Management**

- App whitelisting
    
- Digital signatures
    
- Strong authentication
    

---

## **12.5.12 Mobile Device Protections**

**Threats**

- Theft / Loss
    
- Unauthorized access
    
- OS vulnerabilities
    
- App risks
    
- Network attacks
    

**Dangerous practices**

- **Jailbreaking** (iOS)
    
- **Rooting** (Android)
    
- **Sideloading** (installing unapproved apps)
    

**Protections**

- Screen lock (password/PIN)
    
- Biometrics
    
- Context-aware authentication
    
- Remote wipe
    
- Full device encryption
    

---

## **12.5.13 GPS Tracking**

- GPS gives ±5m location accuracy.
    
- Apps use **geolocation / geofencing**.
    
- Push notifications may use location.
    
- Attackers now exploit push notifications for phishing and data capture.
    

---
