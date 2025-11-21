
# **8.7.1 Installing and Running Applications on a Linux Host — Summary**

Linux uses **package managers** to install applications along with all their dependencies in the correct file system locations.

### **Common Package Managers**

- **pacman** → Arch Linux
    
- **dpkg** and **apt / apt-get** → Debian & Ubuntu
    

### **Key Commands (apt-get)**

**`sudo apt-get update`**

- Downloads the latest package lists from repositories.
    
- Updates the local package database.
    

**`sudo apt-get upgrade`**

- Upgrades installed packages to their latest versions.
    
- Downloads new versions + applies dependency changes.
    

Package managers make installation safer and reduce errors by automatically organizing files and dependencies.

---

# **8.7.2 Keeping the System Up to Date — Summary**

Linux systems can also be updated via a **graphical interface (GUI)**.

Example (Ubuntu):

- Open **Software Updater**.
    
- Check for new updates.
    
- Install updates manually.
    

Keeping Linux updated is critical for:

- security patches
    
- performance improvements
    
- bug fixes
    

---

# **8.7.3 Processes and Forks — Summary**

Linux uses processes to run all programs. The **top** command displays real-time information about system activity.

### **What top Shows**

- Load average
    
- CPU usage (user, system, idle…)
    
- Memory & swap usage
    
- Total processes (running, sleeping, zombie)
    
- Process list with:
    
    - PID
        
    - USER
        
    - CPU %
        
    - Memory %
        
    - Command name
        

### **Forks**

Many applications create new processes by **forking**, meaning:

- One process duplicates itself.
    
- The new process becomes a child process.
    

This is essential for multitasking and running background tasks.

---

# **8.7.4 Malware on a Linux Host — Summary**

Linux is generally secure due to:

- strong permission model
    
- user privilege separation
    
- reliable file system structure
    

But Linux is **not immune** to malware.

### **Common Attack Vectors**

- Vulnerable services (Apache, SSH, FTP…)
    
- Outdated applications
    
- Open ports with old versions
    
- Exploitable kernel bugs
    

### **Example**

An attacker uses **Telnet to query port 80** and discovers:

```
Server: nginx/1.12.0
```

This reveals:

- The server type
    
- The software version
    
- Potential vulnerabilities to research and exploit
    

### **Defense**

- Keep services updated
    
- Close unused ports
    
- Disable unnecessary services
    

---

# **8.7.5 Rootkit Check — Summary**

A **rootkit** is advanced malware designed to:

- gain unauthorized root-level privileges
    
- hide itself
    
- modify kernel behavior
    
- maintain persistence
    

### **Why Rootkits Are Dangerous**

- They modify core OS components.
    
- They hide their presence by altering logs and system tools.
    
- They can survive reboots.
    

### **Detection**

Because the OS may be compromised, detection often requires:

- booting from **trusted external media**
    
- scanning the disk from outside the infected OS
    

Common methods:

- Signature scanning
    
- Behavioral analysis
    
- File comparison
    
- Memory dump analysis
    

### **chkrootkit**

A common Linux tool that scans for known rootkits.

Example:

```
sudo ./chkrootkit
Checking 'chfn'... not infected
Checking 'cron'... not infected
...
```

⚠️ **Rootkit scanners are not 100% reliable.**  
In many cases, OS reinstallation is the only safe solution.

---

# **8.7.6 Piping Commands — Summary**

**Piping** allows you to chain commands so that the output of one becomes the input of another.

Symbol: **`|`**

### **Example**

List files, then filter results with grep:

```
ls -l | grep host
```

Output only shows files containing “host”.

Another example:

```
ls -l | grep file
```

Shows only entries with “file”.

### **Why Piping Is Powerful**

- Combine simple tools to create complex operations
    
- Filter, sort, search, modify output dynamically
    
- Essential for automation and scripting
    

Piping is one of the core strengths of the Linux command line.

---

If you're ready, we can continue with **Module 9** or start a new section of Module 8.