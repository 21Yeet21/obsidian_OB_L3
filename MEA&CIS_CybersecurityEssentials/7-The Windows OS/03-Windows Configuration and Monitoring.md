

---

# **7.3.2 Local Users and Domains — Summary**

When Windows is first installed, a **local user account** is created. This account stores:

- Personal settings
    
- Permissions
    
- File locations
    
- User data
    

### **Default Accounts**

- **Administrator** (disabled by default)
    
    - Should remain disabled for security
        
    - Use admin password only when required
        
- **Guest** (disabled by default)
    
    - No password → very insecure
        
    - Provides a temporary, restricted environment
        

### **Groups**

Windows organizes permissions using **groups**:

- Users inherit group permissions
    
- A user may belong to multiple groups
    
- “Deny” permissions override “Allow”
    
- Managed using **lusrmgr.msc**
    

### **Domains**

- Centralized authentication managed by **Domain Controllers (DCs)**
    
- Store users, computers, policies, and security settings
    
- Domain settings override local settings
    
- Used in enterprise environments
    

---

# **7.3.3 CLI and PowerShell — Summary**

Windows provides two command environments:

## **Command Line Interface (cmd.exe)**

- Run programs, manage files, navigate directories
    
- Supports batch scripts
    
- Paths are **case-insensitive**
    
- Device references use **drive letters (C:, D:\ etc.)**
    
- Uses `/` for command switches
    
- Tab autocompletion
    
- History accessible with ↑ and ↓ arrows
    

## **PowerShell**

More powerful than CMD; used for automation and system management.

PowerShell supports:

- **Cmdlets**
    
- **PowerShell scripts (.ps1)**
    
- **Functions**
    

To use help:

- `Get-Help command`
    
- `Get-Help command -examples`
    
- `Get-Help command -detailed`
    
- `Get-Help command -full`
    

---

# **7.3.4 Windows Management Instrumentation (WMI) — Summary**

WMI is used to manage and monitor **local and remote computers**.

### **Capabilities**

- Collect hardware/software info
    
- Monitor system health
    
- Automate administrative tasks
    

### **Access**

Control Panel → Administrative Tools → Computer Management → WMI Control

### **WMI Control Tabs**

- **General** — system summary
    
- **Backup/Restore** — WMI data backup
    
- **Security** — access permissions
    
- **Advanced** — namespaces configuration
    

### **Security Risk**

Attackers may use WMI to:

- Run remote commands
    
- Modify registry
    
- Avoid detection (traffic appears legitimate)
    

→ **Limit WMI access strictly.**

---

# **7.3.5 The net Command — Summary**

`net` is a powerful administrative command with many subcommands.

### Examples of what it can manage:

- Accounts
    
- Sessions
    
- Shares
    
- Services
    
- Network resources
    
- Remote computers
    

Examples of subcommands:

|Command|Purpose|
|---|---|
|`net accounts`|Password/logon policies|
|`net session`|View active sessions|
|`net share`|Manage shared folders|
|`net start`|Start a service|
|`net stop`|Stop a service|
|`net use`|Connect to network resources|
|`net view`|List network devices|

Run **`net help`** to list all commands; **`net help <command>`** for detailed help.

---

# **7.3.6 Task Manager & Resource Monitor — Summary**

Windows provides two key monitoring tools:

---

## **Task Manager**

### Tabs & Purposes

**Processes**

- Shows running apps and background processes
    
- Displays CPU/memory/disk/network usage
    

**Performance**

- Real-time charts for CPU, RAM, disk, network
    

**App History**

- Resource usage over time
    

**Startup**

- Programs configured to start automatically
    

**Users**

- Shows logged-in users and their resource usage
    

**Details**

- Advanced process controls (priority, affinity, wait chain)
    

**Services**

- View/manage Windows services
    

---

## **Resource Monitor**

Provides deeper technical details:

### Tabs

- **Overview** — general summary
    
- **CPU** — threads, services, handles, modules
    
- **Memory** — detailed RAM statistics
    
- **Disk** — read/write operations per process
    
- **Network** — TCP connections, ports, listening services
    

Useful for troubleshooting malware or performance issues.

---

# **7.3.7 Networking — Summary**

Networking in Windows is managed through the **Network and Sharing Center**.

### Capabilities

- View active network connection
    
- Configure adapters
    
- Change sharing settings
    
- Run diagnostics
    
- Create new connections
    

### **Change Adapter Settings**

- Right-click adapter → Properties
    
- Configure IPv4/IPv6
    
- Choose DHCP or manual addressing
    

### **Useful Commands**

- `nslookup` — test DNS resolution
    
- `netstat` — show active connections, ports, states
    
- `netsh` — configure network settings via CLI
    

---

# **7.3.8 Accessing Network Resources — Summary**

Windows uses **SMB** and **UNC paths** to access shared files.

### **UNC Format**

```
\\servername\sharename\file
```

### **Administrative Shares**

Automatically created, hidden shares:

- `C$`, `D$`, `E$` — disk volumes
    
- `ADMIN$` — Windows directory
    
- `PRINT$` — printer drivers
    

Only administrators can access these.

### **Remote Desktop Protocol (RDP)**

Used to remotely control another machine.

Security considerations:

- RDP is a common attack vector
    
- Limit exposure to the internet
    
- Use strong authentication
    

---

# **7.3.9 Windows Server — Summary**

Windows Server is designed for enterprise environments and provides many services.

### **Examples of Windows Server roles**

**Network Services**

- DNS
    
- DHCP
    
- Terminal Services
    
- Network Controller
    
- Hyper-V virtualization
    

**File Services**

- SMB
    
- NFS
    
- DFS
    

**Web Services**

- FTP
    
- HTTP
    
- HTTPS
    

**Management**

- Group Policy
    
- Active Directory Domain Services (AD DS)
    

Windows Server plays a central role in both infrastructure and security.

---

If you want, I can continue with **Module 8**, or convert all of Module 7 into a **cheat sheet** or **diagram-style overview** for Obsidian.