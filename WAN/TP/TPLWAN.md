here is the corrected version


| **R2 ↔ R3** | R2→ Se1/0 R3 → Se1/0 | R2→ Fa2/0 R2 → Fa2/0 |     |
| ----------- | -------------------- | -------------------- | --- |
now take notes of those , ill upload the config files of the original exercice and you do conversion make sure you are 100 percent sure always get back to those informations 




Perfect 🔥 — since your configuration is complete, the final step is **systematic verification**:  
You’ll test **MPLS**, **IGP (OSPF)**, **MP-BGP**, and **VPN (VRF reachability)** — step by step.

Below is the **official test & verification plan** for your topology (R1–R7).  
Everything is grouped logically so you can follow easily.

---

## 🧭 **Step 1 – Base Connectivity**

🔹 **Check all interfaces**

```bash
show ip interface brief
```

✅ All connected FastEthernet interfaces must be **UP/UP**.

🔹 **Check Loopback reachability**

```bash
ping 10.10.1.1
ping 10.10.2.2
ping 10.10.3.3
ping 10.10.4.4
ping 10.10.5.5
```

➡️ Perform this from **R1** — all P and PE Loopbacks must reply.

---

## ⚙️ **Step 2 – IGP (OSPF) Verification**

Run on any PE/P router (e.g. R1 or R2):

```bash
show ip ospf neighbor
```

✅ You should see adjacency between:

- R1 ↔ R2
    
- R1 ↔ R3
    
- R2 ↔ R3
    
- R2 ↔ R4
    
- R3 ↔ R5
    

Each should show **FULL/ -** state.

Check routing table:

```bash
show ip route ospf
```

✅ You must see routes to all 10.10.x.x networks learned by OSPF.

---

## 🎯 **Step 3 – MPLS Verification**

🔹 Check MPLS neighbors:

```bash
show tag-switching tdp neighbor
```

✅ Every router R1–R5 must have adjacency to its direct neighbors.

🔹 Verify MPLS forwarding entries:

```bash
show tag-switching forwarding-table
```

✅ You must see label entries for all 10.10.x.x prefixes.

---

## 🌍 **Step 4 – MP-BGP (VPNv4) Verification**

Run this on any PE (R1, R4, R5):

```bash
show ip bgp vpnv4 all summary
```

✅ All BGP neighbors (loopbacks of PEs) must be in **Established** state.

Check advertised VPNv4 routes:

```bash
show ip bgp vpnv4 all
```

✅ You should see routes for:

- VRF BLUE
    
- VRF RED
    
- VRF GREEN
    

Example lines:

```
Route Distinguisher: 100:2 (RED)
*>i100.10.5.5/32 via 10.10.5.5
*>i100.10.7.7/32 via 10.10.5.5
```

---

## 🧩 **Step 5 – VRF Table Verification**

Run on **R4 (PE)** and **R5 (PE)**:

### VRF BLUE

```bash
show ip route vrf BLUE
```

### VRF RED

```bash
show ip route vrf RED
```

### VRF GREEN

```bash
show ip route vrf GREEN
```

✅ Each VRF should display:

- Directly connected Loopbacks
    
- Remote site routes imported via MP-BGP  
    (e.g., routes of R6 for GREEN or R7 for RED)
    

---

## 🛰 **Step 6 – VPN Connectivity Tests**

These are **end-to-end functional pings** between CE sites through the MPLS backbone.

### 🟢 VRF GREEN

From **R4** or **R6**:

```bash
ping vrf GREEN 100.10.6.6
ping vrf GREEN 100.10.4.4
```

✅ Expected: Successful — verifies RIP between CE–PE and MP-BGP redistribution.

---

### 🔴 VRF RED

From **R5**:

```bash
ping vrf RED 100.10.7.7
ping vrf RED 100.10.5.5
```

✅ Expected: Success — confirms eBGP between R5 (PE) and R7 (CE).

Then from **R7**:

```bash
ping 100.10.5.5
```

✅ Expected: Success — proves VPN RED path OK.

---

### 🔵 VRF BLUE

From **R4** or **R5**:

```bash
ping vrf BLUE 100.10.4.4
ping vrf BLUE 100.10.5.5
```

✅ Expected: Success — both are internal (PE–PE VRF).

---

## 🔍 **Step 7 – Label Inspection for VPN Routes**

To confirm MPLS label assignment for VPN routes:

```bash
show ip bgp vpnv4 all tags
```

✅ Each VPNv4 route should show:

```
Network Next Hop In tag/Out tag
100.10.57.0/24 10.10.5.5 notag/28
```

Meaning: the route is labeled and distributed correctly.

---

## 🧠 **Optional Troubleshooting Commands**

If something fails:

```bash
show ip cef vrf <vrf-name>
show ip route vrf <vrf-name>
show ip bgp vpnv4 all neighbors
show tag-switching interface
debug mpls packet
debug ip routing
```

---

## ✅ **Expected End-State Summary**

|Verification|Command|Expected Result|
|---|---|---|
|Interfaces|`show ip int brief`|All UP/UP|
|OSPF|`show ip ospf neighbor`|FULL adjacency|
|MPLS|`show tag-switching tdp neighbor`|All neighbors UP|
|MP-BGP|`show ip bgp vpnv4 all summary`|All in Established|
|VRF Routing|`show ip route vrf <vrf>`|Routes from remote CEs visible|
|VPN Connectivity|`ping vrf <vrf> <dest>`|Success across MPLS backbone|

---

Would you like me to add **a short “expected output example”** (e.g., what `show ip route vrf RED` or `show ip bgp vpnv4 all` should look like on R5)?  
That helps you visually confirm each table matches your result.