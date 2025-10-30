

---

## 🧾 **Lab Summary: Docker Introduction**

### 🧱 **Objective**

This lab introduces **Docker fundamentals**, using a **CentOS 7 VM** to explore:

- Docker Engine operation
    
- Images and containers
    
- Docker Hub and image registries
    
- Container isolation and management
    

---

### ⚙️ **1. Installation and First Container**

**Steps:**

- Removed old Docker versions
    
- Added the official Docker repository
    
- Installed the required packages:
    
    ```bash
    sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```
    
- Enabled and started Docker:
    
    ```bash
    sudo systemctl enable docker --now
    ```
    

**Test:**

- Ran the first container:
    
    ```bash
    docker run hello-world
    ```
    

✅ **Result:** Docker downloaded the image from Docker Hub, created a container, executed it, and displayed the “Hello from Docker!” message.

---

### 🌐 **2. Running a Web Container**

**Command:**

```bash
docker run -d -p 80:80 docker/getting-started
```

**Explanation:**

- `-d` → run in background (detached mode)
    
- `-p 80:80` → map port 80 of the host to port 80 in the container
    
- Opens the Docker tutorial web app via:
    
    ```
    http://localhost/tutorial/
    ```
    

---

### 📦 **3. Working with Docker Images**

**Pulling an image:**

```bash
docker image pull alpine
```

**Listing images:**

```bash
docker image ls
```

**Inspecting an image:**

```bash
docker image inspect alpine
```

✅ **Result:** Alpine (a minimal Linux image) is lightweight and ideal for testing.

---

### 🧰 **4. Running and Exploring Containers**

**Examples:**

- Run a command:
    
    ```bash
    docker container run alpine ls -l
    ```
    
- Execute inline:
    
    ```bash
    docker container run alpine echo "hello from alpine"
    ```
    
- Start an interactive shell:
    
    ```bash
    docker container run -it alpine /bin/sh
    ```
    

**Concept:**

- Each command creates a **new isolated container instance**.
    
- Once the command ends, the container **stops automatically**.
    

---

### 🔒 **5. Container Isolation**

**Test:**

- Created a file in one container:
    
    ```bash
    docker container run -itd --name testco alpine
    docker container attach testco
    echo hello > hello.txt
    ```
    
- Then ran another Alpine container and confirmed the file wasn’t there.
    

✅ **Conclusion:**  
Each container has its **own isolated filesystem and process space**, even when based on the same image.

---

### 🧩 **6. Managing Containers**

**List containers:**

```bash
docker container ls -a
```

**Reattach or execute commands:**

```bash
docker container exec <container_id> ls
docker container attach <container_id>
```

**Keep a container running (detach without stopping):**

- `Ctrl + P`, then `Ctrl + Q`
    

**Stop or kill a container:**

```bash
docker stop <container_id>
docker kill <container_id>
```

**Difference:**

- `stop` → sends SIGTERM, then SIGKILL after timeout
    
- `kill` → sends SIGKILL immediately
    

---

### 🧾 **7. Naming Containers**

To manage containers easily:

```bash
docker container run -it --name test1 alpine /bin/ash
```

Then use the name in other commands:

```bash
docker container top test1
docker container stats test1
docker container stop test1
docker container rm test1
```

✅ **Tip:** You must stop a container before removing it.

---

### 💡 **8. Key Takeaways**

- **Images** = Blueprints for containers
    
- **Containers** = Isolated runtime environments
    
- **Docker Engine** = Runs and manages containers
    
- **Docker Hub** = Central repository for sharing images
    
- **Isolation** = Each container runs independently, ensuring security and separation
    

---

### ✅ **Final Results**

After completing this lab, you can:

- Install and configure Docker
    
- Pull and manage images from Docker Hub
    
- Run and interact with containers
    
- Understand container lifecycle and isolation
    
- Manage containers using CLI commands
    

---
