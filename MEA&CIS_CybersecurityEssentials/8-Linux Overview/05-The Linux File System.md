

---

# **8.5.1 File System Types in Linux — Summary**

Linux supports many file system types, each with different performance, reliability, and usage characteristics. Administrators choose the file system based on speed, stability, security, and storage medium.

### **Common Linux File Systems**

**• ext2**

- Older default file system (replaced by ext3).
    
- No journaling → faster, fewer writes → ideal for **flash storage**.
    
- Minimizes wear on USB drives/SD cards.
    

**• ext3**

- ext2 + **journaling** (helps prevent corruption after crashes).
    
- Keeps a log of pending operations for recovery.
    
- Supports files up to **32 TB**.
    

**• ext4**

- Successor to ext3, with major performance improvements.
    
- Supports very large file sizes and modern storage features.
    
- Can operate **with or without journaling**.
    

**• NFS (Network File System)**

- Lets users access files **over the network** as if they were local.
    
- Open standard supported by many OSes.
    

**• CDFS**

- File system designed for **CD/DVD optical media**.
    

**• Swap**

- Disk space used when RAM is full.
    
- Very slow compared to RAM → backup only, not main memory.
    

**• HFS+**

- Apple’s older file system (macOS).
    
- Linux can mount it for read/write operations.
    

**• APFS**

- Apple’s modern file system for SSD/flash.
    
- Strong encryption and advanced features.
    

**• MBR (Master Boot Record)**

- Stored in the first sector of a disk.
    
- Contains partition info and the initial boot loader.
    

---

### **Mounting File Systems**

"Mounting" means attaching a file system to a directory (mount point).  
Example: the **/ (root)** directory usually sits on `/dev/sda1`.

Running `mount` with no options lists all mounted file systems.

Example from the output:

- `/dev/sda1 on / type ext4` → the root file system is ext4.
    
- Many other mounted items are internal kernel or virtual file systems.
    

---

# **8.5.2 Linux Roles and File Permissions — Summary**

Linux enforces security using file permissions. Every file has three permission groups:

- **User** (owner)
    
- **Group**
    
- **Others** (everyone else)
    

Permissions are:

- **r** = read
    
- **w** = write
    
- **x** = execute
    

### **Example Output**

```
-rwxrw-r-- 1 analyst staff 253 May 20 12:49 space.txt
```

### **Interpretation**

- `-` → regular file (a `d` indicates a directory)
    
- **User**: rwx → full permissions
    
- **Group**: rw- → read/write
    
- **Others**: r-- → read only
    
- Number of links: `1`
    
- Owner: `analyst`
    
- Group: `staff`
    
- Size: 253 bytes
    
- Last modified: May 20
    
- Filename: space.txt
    

### **Key Points**

- Only the **root user** can override any file permission.
    
- Permissions are fundamental and cannot be bypassed by normal users.
    
- Permissions ensure users cannot access files they are not authorized to use.
    

---

# **8.5.3 Hard Links and Symbolic Links — Summary**

Linux supports two types of links: **hard links** and **symbolic (soft) links**.

---

## **Hard Links**

A hard link is **another name** for the same physical file (same inode).

### **Properties**

- Created using: `ln file1 file2`
    
- Both filenames point to the **same data**.
    
- Editing one changes the other.
    
- Deleting one **does not delete the data** until all hard links are removed.
    
- Cannot link across different file systems.
    
- Cannot link to directories.
    

### **Example Behavior**

- space.txt and space.hard.txt both show `2` links.
    
- Adding text to one updates both.
    
- Deleting one does not affect the other.
    

---

## **Symbolic (Soft) Links**

A symbolic link is a **pointer** to another file (similar to a shortcut).

### **Properties**

- Created using: `ln -s target linkname`
    
- Shows the target in `ls -l`:  
    `mytest.txt -> test.txt`
    
- Editing the symlink edits the original file.
    
- If the original file is deleted → _symlink breaks_.
    
- Can link across file systems.
    
- Can link directories.
    
- Easier to locate and manage.
    

### **Example Behavior**

- Editing mytest.txt also edits test.txt.
    
- Deleting test.txt makes mytest.txt invalid.
    

---

If you're ready, we can continue with **8.6 (Processes, System Monitoring, etc.)** or jump directly to the next module.