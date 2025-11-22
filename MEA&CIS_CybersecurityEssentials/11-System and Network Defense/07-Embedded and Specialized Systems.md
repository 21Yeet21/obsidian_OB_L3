
---

## **12.7.2 Threats to Key Industry Sectors**

Critical infrastructures use **SCADA/ICS** systems (energy, water, manufacturing, communications).  
Attacks like **Stuxnet** proved malware can disrupt or destroy physical systems.

**Impact of attacks:**

- Shutdown of industrial processes
    
- Damage to equipment
    
- Loss of service (power, water, comms)
    
- Economic damage
    
- Safety risks
    

**Prevention:**

- Network segmentation
    
- Patching & updates
    
- Monitoring ICS traffic
    
- Physical security
    
- Strong authentication
    
- Dedicated isolated networks for SCADA
    

---

## **12.7.3 The Emergence of IoT**

IoT = billions of Internet-connected devices (cars, cameras, smart home, sensors…).

**Risks:**

- Massive increase in attack surface
    
- Weak default credentials
    
- Outdated firmware
    
- Devices used in malware botnets (e.g., huge DDoS attacks)
    
- Huge data growth (Big Data)
    

**Security requirements:**

- Devices must support firmware updates
    
- Change all default admin passwords
    
- Secure remote access
    
- Secure network where IoT is deployed
    

---

## **12.7.4 Embedded Systems**

Used in smart TVs, medical devices, HVAC, industrial equipment, vehicles.

**Attack types:**

- **Timing attacks** (side-channel attacks)
    
- Power consumption, electromagnetic leaks, timing responses exploited
    
- Exploiting vulnerabilities in hardware/firmware
    

**Mitigation:**

- System-on-Chip (SoC) with better integration
    
- Lower cost & power, but:
    
    - Often poor authentication
        
    - Often cannot be updated
        
    - Requires “implied trust” due to no formal security verification
        

---

## **12.7.5 Securing IoT Devices**

IoT deployed for automation, sensing, remote monitoring.

Security steps:

- Secure the wireless network
    
- Inventory all connected devices
    
- Understand what each device does
    
- Install security software when possible
    
- Secure smartphones/apps controlling IoT
    

---

## **12.7.6 IoT Communication & Scanning**

Tools like **Shodan** can scan for vulnerable IoT devices online.

IoT connectivity methods:

- Cellular (4G/5G)
    
- Radio
    
- **Zigbee** (WPAN protocol)
    

---

## **12.7.8 VoIP Equipment & Security**

### **Equipment needed**

- Internet connection
    
- One of:
    
    - Traditional phone + VoIP adapter
        
    - VoIP phone
        
    - VoIP software on computer
        

### **Is VoIP secure?**

- Depends on network security
    
- Attacks: eavesdropping, call hijacking, DoS, registration spoofing
    

### **Protection measures**

- Encrypt voice packets
    
- Use SSH to secure gateways/switches
    
- Change all default passwords
    
- Use IDS to detect ARP poisoning
    
- Strong authentication
    
- VoIP-aware firewalls
    

---

## **12.7.10 Special-Purpose Embedded Systems**

Industries using embedded devices:

- Medical (pacemakers, pumps…)
    
- Automotive (ECUs, sensors)
    
- Aviation (navigation, sensors)
    

Each has strict safety/security requirements due to real-world impact if compromised.

---

## **12.7.11 Deception Technologies**

Used to distract attackers and study their methods.

Two main techniques:

### **1. Honeypots**

- Fake systems that attract attackers
    
- Allow monitoring of malicious behavior
    
- Provide early warning signals
    

### **2. Honey files / honey tokens**

- Fake files, credentials, or data
    
- Trigger alerts if accessed
    
- Reveal intruder presence
    

Deception = “fake environment layer” added to confuse attackers.

---

