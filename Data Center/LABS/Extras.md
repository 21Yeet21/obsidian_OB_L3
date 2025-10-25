

---

## 🧾 **Summary: Accessing a Docker Container and Checking Its IP**

### 🐳 **1️⃣ Run the Container**

You started a Docker container using the **getting-started** image:

```bash
docker run -d -p 80:80 docker/getting-started
```

**What this does:**

- `-d` → runs the container in the background (detached mode).
    
- `-p 80:80` → maps port **80 on your host** to port **80 inside the container**.
    
- `docker/getting-started` → the official Docker tutorial image.
    

✅ **Result:**  
You can now access the web application by visiting:

```
http://localhost
```

or, if on a remote server:

```
http://<host_IP>
```

---

### 🌐 **2️⃣ Inspect the Default Docker Network**

You checked the **default network** configuration:

```bash
docker network inspect bridge
```

**Purpose:**

- Shows all containers connected to the `bridge` network (the default one).
    
- Displays IP addresses assigned by Docker’s internal DHCP.
    

Example output section:

```json
"Containers": {
    "7e81cf40ffaa": {
        "Name": "awesome_container",
        "IPv4Address": "172.17.0.2/16"
    }
}
```

✅ **Result:**  
You obtained the **container’s internal IP** (`172.17.0.2`) used for communication inside Docker networks.

---

### 🔍 **3️⃣ Access Container Shell**

Since the container didn’t have **bash**, you used **sh**:

```bash
docker exec -it 7e81cf40ffaa sh
```

✅ **Result:**  
You entered the container’s shell (usually `/ #` prompt for minimal images).

Then, you verified the container’s IP inside:

```bash
ip a
```

or

```bash
hostname -I
```

Output example:

```
172.17.0.2
```

---

### 💡 **4️⃣ Two Ways to Access the Container**

You confirmed that:

1. From your **host**, you can access it via:
    
    ```
    http://localhost
    ```
    
    (because of port mapping `-p 80:80`)
    
2. From **another container on the same Docker network**, you can reach it via:
    
    ```
    http://172.17.0.2
    ```
    

---

### ✅ **5️⃣ Summary Table**

|Action|Command|Purpose|Result|
|---|---|---|---|
|Run container|`docker run -d -p 80:80 docker/getting-started`|Start container and expose web service|Accessible via `localhost`|
|Check Docker networks|`docker network inspect bridge`|View connected containers and their IPs|Found container’s internal IP|
|Enter container shell|`docker exec -it <container_id> sh`|Open interactive shell (for minimal images)|Verified internal IP using `ip a`|
|Verify connection|`curl localhost` or browser|Test web access|Works locally via port mapping|

---

