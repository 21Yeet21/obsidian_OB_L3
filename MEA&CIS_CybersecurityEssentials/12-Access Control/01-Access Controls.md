

---

## **13.1.2 Physical Access Controls**

Physical controls **prevent unauthorized physical access** to buildings, rooms or equipment.

**Examples:**

- Guards
    
- Fences / perimeter security
    
- Motion detectors
    
- Laptop locks
    
- Locked doors
    
- Swipe cards / badge access
    
- Guard dogs
    
- CCTV cameras
    
- Mantraps
    
- Intrusion alarms
    

Purpose: **control who enters, where they enter, and when they enter.**

---

## **13.1.3 Logical Access Controls**

Logical controls use **technology** to regulate access to systems, data and networks.

**Examples:**

- Encryption
    
- Smart cards
    
- Passwords / PINs
    
- Biometrics
    
- ACLs (Access Control Lists)
    
- Protocols (rules governing data exchange)
    
- Firewalls
    
- Routers
    
- IDS (Intrusion Detection Systems)
    
- Clipping levels (error thresholds that trigger alerts)
    

They ensure **identification, authentication, authorization, accountability**.

---

## **13.1.4 Administrative Access Controls**

Administrative controls = **policies, procedures, standards and guidelines** that guide how access is granted, managed and monitored.

Examples (training, policies, background checks, onboarding rules)…


---

## **13.1.5 Administrative Access Controls in Detail (AAA)**

AAA = **Authentication, Authorization, Accounting**

### **1. Authentication – verifying identity**

Users prove identity using:

- Something they **know** → password, PIN
    
- Something they **have** → smart card, token
    
- Something they **are** → fingerprint, face, retina
    

2FA uses **two different categories**.

---

### **2. Authorization – determining access level**

Defines what the authenticated user _can do_:

- Read / write / create / delete
    
- Access rules based on ACLs
    
- Time-based access (e.g., only during work hours)
    

Group policies & role-based rules determine what resources users can access.

---

### **3. Accounting – tracking user activity**

Tracks:

- Login times
    
- Access attempts
    
- Commands executed
    
- Files modified
    

Used for:

- Auditing
    
- Incident investigation
    
- Billing / usage tracking
    

Accounting = _trace every action to a user or process._

---

## **13.1.6 Identification**

Identification = **unique identity claim** such as username, biometric ID, PIN, or smart card.

It links actions to the correct user and enforces authorization policies.

---

## **13.1.8 Federated Identity Management**

Federated identity = one set of credentials used across multiple systems.

Examples:

- Sign in to multiple websites using Google or Facebook login.
    

Advantages:

- Single sign-on experience
    

Risks:

- Larger attack surface
    
- Cascading breaches
    
- Sensitive ID data shared between organizations
    

Best practice:

- Tie federated login to **an authorized device**.
    

---

## **13.1.9 Authentication Methods**

### **Something You Know**

- Passwords, passphrases, PINs  
    Use strong passwords (length + complexity).  
    Use different passwords for each system.
    

### **Something You Have**

- Smart cards (embedded chip, stores secure data)
    
- Security key fobs (used in 2FA)
    

### **Something You Are**

- Biometrics:
    
    - Physiological: fingerprint, face, retina, DNA
        
    - Behavioral: voice, typing rhythm, gait
        

Biometric systems require:

- Scanner
    
- Conversion software
    
- Stored profile for comparison
    

---

## **13.1.10 Multi-Factor Authentication (MFA)**

MFA = ≥2 authentication factors (e.g., password + smart card + fingerprint)

Examples:

- Online banking (password + SMS code)
    
- ATM (card + PIN)
    

2FA = a **subset** of MFA.

---

## **13.1.12 Authorization (Detailed)**

Authorization happens _after_ authentication.

### **Rules determine**:

- What a user can read / edit / delete
    
- Which resources they can access
    
- When they may access them
    

### **Types of authorization policies**

- **Group membership** (departments, teams)
    
- **Authority-level / role-based** (job position)
    

Authorization is **automatic** once access policies are defined.

---

## **13.1.15 Accountability**

Accountability = **tracking actions → linking them to users → reporting usage**.

**Purpose:**

- Auditing
    
- Detecting abnormal behavior
    
- Investigating incidents
    

**Implementation includes:**

- Logs (login attempts, access logs, transaction logs)
    
- Policies for retention, review, storage
    
- Education & awareness
    
- Legal compliance
    

---

