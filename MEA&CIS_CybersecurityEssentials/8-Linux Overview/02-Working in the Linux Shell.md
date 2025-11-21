

---

# **8.2.2 Basic Commands — Summary**

Linux provides core commands that allow the user to interact with the system. Some fundamental commands include:

### **• `pwd`**

Displays the current directory (print working directory).

### **• `ls`**

Lists files and directories.

### **• `cd`**

Changes directories.

### **• `man <command>`**

Shows the manual page for a command.

### **• `clear`**

Clears the terminal screen.

These commands form the foundation for navigation and interaction in the Linux CLI.

---

# **8.2.3 File and Directory Commands — Summary**

Linux includes several commands for managing files and directories:

### **• `touch <file>`**

Creates an empty file or updates timestamps.

### **• `mkdir <directory>`**

Creates a new directory.

### **• `cp <source> <destination>`**

Copies files or directories.

### **• `mv <source> <destination>`**

Moves or renames files or directories.

### **• `rm <file>` / `rm -r <directory>`**

Deletes files or directories.

### **• `cat <file>`**

Displays the contents of a file.

### **• `file <file>`**

Shows the type of file.

These commands allow users to manipulate the file system effectively.

---

# **8.2.4 Working with Text Files — Summary**

Linux relies heavily on **text-based tools**, especially in remote administration where no GUI is available.

Key points:

### **• Text Editors**

Linux provides many editors, both graphical (Gedit, Kate) and CLI-based (nano, vim).

### **• CLI Editors Are Essential**

When working remotely via **SSH**, the user only has a text terminal — so CLI editors like **nano** are crucial.

### **• nano Editor**

- Fully keyboard-driven
    
- Easy to use
    
- Shortcut bar shown at the bottom (e.g., `Ctrl+O` to save, `Ctrl+W` to search)
    

### **Use Case**

CLI editors are commonly used to edit system config files such as:

- Firewall rules
    
- Network configuration
    
- Service configuration
    

---

# **8.2.5 The Importance of Text Files in Linux — Summary**

Linux treats almost **everything as a file**, including:

- Devices
    
- Memory
    
- Directories
    
- Configuration data
    

This model simplifies management and automation.

### **• Configuration Files**

Most Linux services depend on **plain text configuration files** found mostly in `/etc/`.

Examples include:

- `/etc/hosts` (local hostname mappings)
    
- `/etc/passwd` (user accounts)
    
- `/etc/ssh/sshd_config` (SSH server settings)
    

### **• Editing Config Files**

Requires elevated privileges:

```
sudo nano /etc/hosts
```

Modifying these files allows administrators to customize system behavior precisely.

### **• Why This Matters**

Linux services **read configuration files at startup** → changes directly influence system operation.

---

If you want to continue, send **8.2.6**, or tell me to move to the next module.