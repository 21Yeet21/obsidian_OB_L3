

---

# **8.3.1 Introduction to Client–Server Communications — Summary**

A **server** is a computer running specialized software that provides services to clients over a network. Different services require different server applications, such as:

- File servers (store and share files)
    
- Web servers (deliver web pages)
    
- Email servers
    
- Maintenance/management services (logging, memory, scanning)
    

A **client** is the hardware/software combination used by the user to access these services.

### **Key Idea**

Clients request resources → servers respond and deliver them.  
Example: downloading files from a file server.

---

# **8.3.2 Servers, Services, and Their Ports — Summary**

Different services run on different ports. Ports allow clients to communicate with the correct server application on a machine.

### **Common Services and Ports**

- **HTTP** → port **80**
    
- **HTTPS** → port **443**
    
- **FTP** → ports **20** (data) and **21** (control)
    
- **SSH** → port **22**
    
- **DNS** → port **53**
    
- **SMTP** → port **25**
    
- **IMAP** → port **143**
    
- **POP3** → port **110**
    

Servers listen on these ports, waiting for client requests.

---

# **8.3.3 Clients — Summary**

A **client application** communicates with a server using a well-defined protocol.

Examples:

- **Web browser** → communicates with web server using **HTTP/HTTPS**
    
- **FTP client** → communicates with FTP server to upload or download files
    
- **Email client** → uses SMTP, IMAP, or POP3
    

### **Key Idea**

Clients send requests → servers process them → results are returned.

Example: uploading files from a client to a server for storage.

---

# **8.3.4 Port Scanner Lab (Video)**

This section includes a lab video demonstrating how to use a **port scanner** to detect open ports on a target system.  
(A summary cannot be given because the content is video-based.)

---

If you're ready, send **8.3.5** or tell me to continue with the next module.