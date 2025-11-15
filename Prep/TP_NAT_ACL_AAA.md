
---

# 🧱 **WAN Security Essentials – ACL / AAA / NAT Summary**

---

## 🔹 **I. ACL (Access Control List)**

Used to **filter or control traffic** entering or leaving a router interface.

---

### 🧠 **Concepts**

|Type|Range|Filters By|Typical Use|
|---|---|---|---|
|**Basic ACL**|2000–2999|Source IP only|Simple allow/deny|
|**Advanced ACL**|3000–3999|Source, destination, protocol, ports|Fine-grained control (Telnet, HTTP…)|
|**Layer 2 ACL**|4000–4999|MAC addresses|Local LAN filtering|

---

### ⚙️ **Common Syntax**

#### 🔸 Create an ACL

```bash
[R2]acl 3000
 rule 5 permit tcp source 192.168.1.0 0.0.0.255 destination 10.10.3.1 0 destination-port eq 23
 rule 10 deny ip
```

- `rule <number>`: order of rule (lower = higher priority)
    
- `permit / deny`: action
    
- `source` and `destination`: match IPs
    
- `destination-port eq 23`: specific service (Telnet = TCP 23)
    

---

#### 🔸 Apply ACL to an interface

```bash
[R2]interface GigabitEthernet0/0/3
 traffic-filter inbound acl 3000
```

- `inbound` → filters packets **entering** the interface
    
- `outbound` → filters packets **leaving** the interface
    

✅ _Best practice:_

- **Extended ACLs → close to the source**
    
- **Standard ACLs → close to the destination**
    

---

#### 🔸 View ACL rules

```bash
[R2]display acl 3000
```

---

### 💡 **Notes**

- ACLs are processed **top-down** until a match.
    
- Implicit **deny all** at the end.
    
- Combine ACLs with NAT, QoS, or security features.
    

---

## 🔹 **II. AAA (Authentication, Authorization, Accounting)**

Used to **control user access** to devices or services.

---

### 🧠 **Concepts**

|Term|Description|
|---|---|
|**Authentication**|Verifies who the user is|
|**Authorization**|Defines what the user can do|
|**Accounting**|Tracks what the user did|

---

### ⚙️ **Local AAA Configuration (Telnet Example)**

```bash
[R2]aaa
[R2-aaa]authentication-scheme local-scheme
 authentication-mode local
[R2-aaa]authorization-scheme local-scheme
 authorization-mode local
[R2-aaa]domain datacom
 authentication-scheme local-scheme
 authorization-scheme local-scheme

[R2-aaa]local-user admin@datacom password cipher Huawei@123
[R2-aaa]local-user admin@datacom service-type telnet
[R2-aaa]local-user admin@datacom privilege level 3

[R2]telnet server enable
[R2]user-interface vty 0 4
 authentication-mode aaa
```

✅ **Meaning:**

- Users must log in via AAA authentication.
    
- Local user “admin@datacom” authenticates locally.
    
- Privilege level 3 = full access.
    

---

#### 🔸 View connected AAA users

```bash
[R2]display aaa online-users
```

---

### 💡 **Notes**

- Other authentication modes: `radius`, `hwtacacs`, or `none`.
    
- Used for **Telnet**, **SSH**, **Console**, or **VPN logins**.
    
- More secure than plain “password” login mode.
    

---

## 🔹 **III. NAT (Network Address Translation)**

Used to **translate private IPs into public IPs** for Internet or WAN access.

---

### 🧠 **Concepts**

| Type              | Description                            | Example                                    |
| ----------------- | -------------------------------------- | ------------------------------------------ |
| **Static NAT**    | 1:1 fixed mapping                      | 192.168.1.10 ↔ 1.2.3.10                    |
| **Dynamic NAT**   | Uses public IP pool                    | Multiple private IPs share pool (no ports) |
| **Easy IP (PAT)** | Many-to-one using interface IP & ports | Everyone uses 1.2.3.4                      |
| **NAT Server**    | Port forwarding for inbound access     | 1.2.3.4:2323 → 192.168.1.1:23              |

---

### ⚙️ **Static NAT**

```bash
[R2]nat static global 1.2.3.10 inside 192.168.1.10
```

---

### ⚙️ **Dynamic NAT**

```bash
[R2]nat address-group 1 1.2.3.10 1.2.3.20
[R2]acl 2000
 rule 5 permit source 192.168.1.0 0.0.0.255
[R2]interface G0/0/4
 nat outbound 2000 address-group 1
```

✅ Each private IP gets a random public IP from the pool.  
❌ No port translation (1-to-1).

---

### ⚙️ **Easy IP (PAT)**

```bash
[R2]acl 2000
 rule 5 permit source 192.168.1.0 0.0.0.255
[R2]interface G0/0/4
 nat outbound 2000
```

✅ All private IPs use the **interface’s IP (1.2.3.4)** with different **port numbers**.  
**Many-to-one NAT.**

---

### ⚙️ **NAT Server (Inbound / Port Forwarding)**

```bash
[R2]interface G0/0/4
 nat server protocol tcp global current-interface 2323 inside 192.168.1.1 telnet
```

✅ Maps `1.2.3.4:2323` → `192.168.1.1:23`  
Used when external users must reach internal services (like Telnet/HTTP).

---

### ⚙️ **Verification Commands**

```bash
display nat session all        # Shows active translations
display nat outbound           # Shows NAT mode (Dynamic or Easy IP)
display nat server             # Shows NAT Server entries
```

---

## 🧩 **Quick Comparison**

|Mode|Mapping|Uses Ports?|Common Use|
|---|---|---|---|
|**Static NAT**|1 ↔ 1|No|Fixed host access|
|**Dynamic NAT**|Many ↔ Many|No|Large internal networks|
|**Easy IP (PAT)**|Many ↔ 1|✅ Yes|Small LAN → Internet|
|**NAT Server**|Public ↔ Private|✅ Yes|External access (Telnet, HTTP, etc.)|

---

### ⚠️ **Notes**

- NAT & ACL often work together (ACL defines what traffic gets translated).
    
- PAT (Easy IP) and Dynamic NAT **cannot be combined** on the same interface.
    
- Always apply `nat outbound` on the **WAN-facing (public)** interface.
    

---

## 🧾 **Command Quick Reference (Memorization Sheet)**

|Purpose|Command|
|---|---|
|Create ACL|`acl 3000` → `rule permit tcp source ...`|
|Apply ACL|`int G0/0/3` → `traffic-filter inbound acl 3000`|
|Enable AAA|`aaa` → `authentication-scheme ...`|
|Create user|`local-user user@domain password cipher ...`|
|Enable Telnet|`telnet server enable`|
|Enable NAT Dynamic|`nat outbound <acl> address-group <n>`|
|Enable NAT Easy IP|`nat outbound <acl>`|
|Enable NAT Server|`nat server protocol tcp global current-interface <port> inside <IP> <service>`|
|Verify NAT|`display nat session all`|
|Verify AAA|`display aaa online-users`|
|Verify ACL|`display acl all`|

---

✅ **Final takeaway:**

> - **ACL** = control who can talk
>     
> - **AAA** = control who can log in
>     
> - **NAT** = control who can go out (or come in)
>     

---

Would you like me to make a **10-question quiz** mixing ACL, AAA, and NAT commands (like an HCIA exam practical round) to reinforce this summary?