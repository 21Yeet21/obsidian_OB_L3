
---

## **12.6.2 High Availability Principles**

High availability = systems designed to minimize downtime.

Three core principles:

### **1. Eliminate Single Points of Failure (SPOF)**

- Identify any component whose failure breaks the whole system.
    
- Use redundancy: multiple links, redundant hardware, standby devices.
    

### **2. Provide Reliable Crossover**

- Backup power supplies
    
- Backup communication links
    
- Redundant hardware that can take over instantly
    

### **3. Detect Failures Quickly**

- Continuous monitoring of systems/devices
    
- Automatic failover when an issue appears
    

---

## **12.6.4 Single Points of Failure**

A SPOF = any component where failure stops the entire system.  
Can be hardware, processes, utilities, or data.

Solution:

- Modify design so no process depends on a single element.
    
- Add redundant components to take over automatically.
    

---

## **12.6.6 N+1 Redundancy**

- “N” = number of components required
    
- “+1” = one spare available
    
- Example: 4 tires + 1 spare
    
- Not fully redundant, but protects against one failure.
    

---

## **12.6.7 RAID Basics**

RAID = storing data across multiple disks for performance & availability.

Techniques:

- **Mirroring** → copy of data on a second disk
    
- **Striping** → data split across multiple disks
    
- **Parity** → checksums to recover data
    

RAID ≠ backup.

---

## **12.6.8 Spanning Tree Protocol (STP)**

Redundant links cause loops → network collapse.

STP:

- Blocks redundant links to keep 1 logical path
    
- Recomputes automatically if a link fails
    
- Prevents loops while keeping redundancy ready
    

---

## **12.6.9 Router Redundancy (First-Hop Redundancy)**

If default gateway router fails → network goes down.

Solution:

- Use two routers (active + standby)
    
- Both share a **virtual IP** = the gateway for clients
    
- If active router fails → standby takes over
    

This is **First-Hop Redundancy**.

---

## **12.6.10 Location Redundancy**

Three types:

### **1. Real-Time Replication**

- Synchronized instantly
    
- High bandwidth, low latency
    
- Sites must be close
    

### **2. Near-Real-Time Replication**

- Slight delay
    
- Less bandwidth
    
- Sites can be farther away
    

### **3. Point-in-Time Replication**

- Snapshot backups periodically
    
- Low bandwidth
    
- Not real time
    

---

## **12.6.11 Resilient Design**

Resiliency = designing systems to tolerate failure.

Examples:

- Redundant links + optimized STP
    
- Tuned routing protocols for fast convergence
    
- Understand business needs → choose correct redundancy
    

### **Application Resilience Options**

1. **Fault-tolerant hardware**
    
2. **Cluster architecture**
    
3. **Backup & restore**
    

### **IOS Resilience**

Cisco can store secure copies of:

- IOS image
    
- Running config  
    These can’t be erased, allowing quick recovery.
    

---

## **12.6.12 System & Data Backups**

Backups protect against:

- Theft
    
- Equipment failures
    
- Disaster
    
- Human errors
    

Best practices:

- Regular backups
    
- Off-site storage
    
- Ability to restore to new hardware
    

---

## **12.6.14 Power Considerations**

Electrical issues can destroy equipment.

### **Power Excess**

- Spike = momentary high voltage
    
- Surge = prolonged high voltage
    

### **Power Loss**

- Fault = momentary loss
    
- Blackout = total loss
    

### **Power Degradation**

- Sag/dip = momentary low voltage
    
- Brownout = prolonged low voltage
    
- Inrush current = initial surge when power starts
    

Redundant power feeds + UPS = best practice.

---

## **12.6.17 Managing Physical Facility Threats**

Measures include:

- Access control & CCTV
    
- Guest policies
    
- Pen-testing physical security
    
- Encrypted badges
    
- DRP (Disaster Recovery Planning)
    
- BCP (Business Continuity Planning)
    
- Security awareness training
    
- Asset tagging
    

---
