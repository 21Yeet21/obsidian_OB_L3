
---

# **7.2.1 Hardware Abstraction Layer (HAL) — Summary**

Windows must run on many hardware types. To do this, it uses the:

### **Hardware Abstraction Layer (HAL)**

A software layer between **hardware** and the **Windows kernel**.

![[Pasted image 20251121141912.png]]
### **Purpose**

- Isolates Windows from hardware differences
    
- Handles communication between devices and the OS kernel
    
- Allows Windows to run on diverse systems
    

### **Kernel**

- Core of Windows
    
- Handles memory, processes, I/O, and hardware access
    
- Sometimes communicates directly with hardware, so HAL and kernel depend on each other
    

---

# **7.2.2 User Mode vs Kernel Mode — Summary**

Windows runs code in two CPU modes:

## **User Mode**

- Used by applications
    
- Restricted access
    
- Cannot access hardware directly
    
- Crashes affect only the specific application
    
- Each application gets its **own private address space**
    

## **Kernel Mode**

- Used by OS core and some drivers
    
- Full access to hardware and memory
    
- All kernel-mode code shares the same address space
    
- Crashes affect the entire system (blue screen)
    
- Dangerous driver errors can corrupt the OS
    

---

# **7.2.3 Windows File Systems — Summary**

Different file systems exist across platforms:

### **FAT16 / FAT32**

- Very old
    
- Many limitations (file size, partition size)
    
- Still used on USB drives
    

### **HFS+**

- Used by macOS
    
- Windows cannot write without extra tools
    

### **EXT**

- Used by Linux
    
- Windows can read with special software
    

### **NTFS (Windows default)**

- Most advanced and secure
    
- Supports:
    
    - Large file sizes
        
    - File permissions & ownership
        
    - Timestamps (MACE)
        
    - Reliability and recovery features
        
    - Disk encryption (EFS)
        

### **NTFS Internal Structures**

- **Partition Boot Sector** — boot info & pointer to MFT
    
- **Master File Table (MFT)** — index of all files
    
- **System files** — metadata
    
- **File area** — actual stored files and directories
    

**Note:** Formatting does NOT fully erase data → secure wipe recommended.

---

# **7.2.4 Alternate Data Streams (ADS) — Summary**

NTFS allows storing hidden data inside files using **Alternate Data Streams**.

### **Key Facts**

- Data stored in `filename:streamname`
    
- Main file appears unchanged
    
- ADS is invisible to normal directory listings
    
- Useful for legitimate metadata
    
- **Also used by malware to hide payloads**
    

Example:  
`Testfile.txt:ADS` contains hidden content.

Security tools must check ADS to find hidden malicious data.

---

# **7.2.5 Windows Boot Process — Summary**

Windows uses BIOS or UEFI firmware to start the system.

![[Pasted image 20251121142630.png]]
## **BIOS Path**

1. BIOS init
    
2. POST
    
3. MBR
    
4. Bootmgr.exe
    
5. BCD → Winload.exe
    

## **UEFI Path**

1. UEFI init
    
2. Load EFI files
    
3. Bootmgr.exe
    
4. BCD → Winload.exe
    

## **Common Boot Steps**

- **Bootmgr.exe** switches to protected mode
    
- **BCD** decides:
    
    - Cold boot → Winload.exe
        
    - Resume → Winresume.exe + hiberfil.sys
        
- **Winload.exe**
    
    - Loads drivers
        
    - Verifies digital signatures (KMCS)
        
    - Loads ntoskrnl.exe
        
- **Ntoskrnl.exe** starts the kernel + HAL
    
- **SMSS** creates user session and starts Winlogon
    
- User login begins
    

---

# **7.2.6 Windows Startup — Summary**

Startup programs and services are controlled by registry keys:

### **Main Locations**

- **HKEY_LOCAL_MACHINE** — system-wide startup
    
- **HKEY_CURRENT_USER** — user-specific startup
    

### **Startup Entry Types**

- Run
    
- RunOnce
    
- RunServices
    
- RunServicesOnce
    
- Userinit
    

### **Managing Startup**

Use **Msconfig.exe** for:

- Selecting startup mode (Normal / Diagnostic / Selective)
    
- Managing boot entries
    
- Viewing services
    
- Opening Task Manager to control app startup
    

---

# **7.2.7 Windows Shutdown — Summary**

Proper shutdown ensures data safety.

### **Shutdown Order**

1. Close user-mode applications
    
2. Close kernel-mode processes
    

If user-mode hangs → Windows prompts  
If kernel-mode hangs → shutdown freezes → manual power-off required

### **Shutdown Options**

- **Shutdown** (power off)
    
- **Restart**
    
- **Hibernate** (save RAM state to disk → resume instantly)
    

Shutdown methods include:

- Start menu
    
- Shutdown command
    
- Ctrl+Alt+Delete → Power
    

---

# **7.2.8 Processes, Threads, and Services — Summary**

### **Processes**

- Running programs
    
- Each process has at least one **thread**
    
- Threads run the program instructions
    

### **Threads**

- Multiple threads = multitasking
    
- Number of simultaneous threads depends on CPU cores
    

### **Services**

- Background processes
    
- Support OS and applications
    
- Can be:
    
    - Automatic
        
    - Manual
        
    - Disabled
        

Misconfiguring services can break core features.

**Tools:**

- Task Manager (Processes)
    
- Services.msc (Service control)
    

---

# **7.2.9 Memory Allocation & Handles — Summary**

Windows uses **virtual memory** for processes.

### **Virtual Address Space**

- 32-bit: 4 GB
    
- 64-bit: ~8 TB
    

Each process runs in its own isolated memory space.

### **Kernel Resources**

- Cannot be accessed directly
    
- Must use **handles**
    
    - Virtual references that allow safe controlled access
        

### **RAMMap Tool**

- Shows how Windows allocates memory
    
- Useful for diagnostics and forensics
    
- Part of Sysinternals Suite
    

---

# **7.2.10 Windows Registry — Summary**

The registry stores **all system, user, hardware, and application configurations**.

### **Structure**

- **Hives**
    
- **Keys**
    
- **Subkeys**
    
- **Values (REG_SZ, REG_DWORD, REG_BINARY)**
    

### **Main Hives**

- **HKEY_CURRENT_USER**
    
- **HKEY_USERS**
    
- **HKEY_CLASSES_ROOT**
    
- **HKEY_LOCAL_MACHINE**
    
- **HKEY_CURRENT_CONFIG**
    

### **Security Importance**

- Malware often adds startup entries
    
- Registry stores:
    
    - Device history
        
    - File access history
        
    - Application behavior
        
    - User activity
        
- Critical for forensic investigations
    

### **Editing**

- `regedit.exe`
    
- Dangerous — incorrect changes can break the entire system
    

---

If you want, I can continue with **Module 7.3**, or generate a **diagram-style cheat sheet** for all of Module 7.