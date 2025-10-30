Here’s a **clear and complete summary** of your **Lab – 4 Docker Volumes (v22)** by _Elies Jebri_ 👇

---

## 🧱 **Objectif du lab**

Comprendre et manipuler les **volumes Docker**, utilisés pour **stocker des données en dehors des conteneurs** et permettre la **persistance** ou le **partage de fichiers** entre conteneurs.

---

## ⚙️ **1. Qu’est-ce qu’un volume Docker ?**

Un **volume Docker** est un dossier stocké **sur la machine hôte**, monté dans un conteneur.

- Il **n’est pas supprimé** lorsque le conteneur est arrêté.
    
- Il permet de **partager des données** entre plusieurs conteneurs.
    

📍 Les volumes se trouvent généralement dans :

```
/var/lib/docker/volumes/<volume_name>/_data
```

---

## 🧾 **2. Créer et gérer un volume avec Docker**

### 🔹 Créer un volume nommé :

```bash
docker volume create --name data-volume
```

### 🔹 Lister les volumes :

```bash
docker volume ls
```

### 🔹 Inspecter un volume :

```bash
docker volume inspect data-volume
```

→ Affiche le **point de montage** (`Mountpoint`) du volume sur l’hôte.

---

## 🧱 **3. Utiliser un volume avec un conteneur**

### 🔹 Exemple :

```bash
docker run -it --name my-volume-test -v data-volume:/data centos /bin/bash
```

Vérifier le montage :

```bash
df -Th /data
```

---

### 🔹 Supprimer un volume :

> ⚠️ Le volume doit être **libéré** avant suppression (conteneur arrêté et supprimé).

```bash
docker stop my-volume-test
docker rm my-volume-test
docker volume rm data-volume
```

---

## 🗂️ **4. Créer un volume en liant un dossier hôte (Bind Mount)**

### 🔹 Étapes :

```bash
mkdir /tmp/hostvolume
echo "Hello World" > /tmp/hostvolume/host-hello.txt
```

### 🔹 Lancer le conteneur :

```bash
docker run -it --name my-directory-test -v /tmp/hostvolume:/containervolume centos /bin/bash
```

Vérifier :

```bash
ls /containervolume
# host-hello.txt
```

Créer un fichier depuis le conteneur :

```bash
echo "Hello from container" > /containervolume/container-hello.txt
```

→ Ces fichiers apparaissent aussi sur l’hôte :

```bash
ls /tmp/hostvolume
# container-hello.txt  host-hello.txt
```

---

## 🧩 **5. Créer un volume via Dockerfile**

### 🔹 Dockerfile :

```dockerfile
FROM centos
VOLUME /myvolume
```

### 🔹 Build & run :

```bash
docker build -t dockerfile-volumetest .
docker run -it --name my-dockerfile-test dockerfile-volumetest /bin/bash
```

Créer un fichier dans le volume :

```bash
echo "Hello World" > /myvolume/dockerfile-container-hello.txt
```

Trouver le point de montage sur l’hôte :

```bash
docker inspect my-dockerfile-test | grep -A 10 Mounts
```

---

## 🔗 **6. Partage d’un volume entre plusieurs conteneurs**

### 🔹 Créer un répertoire partagé :

```bash
mkdir /tmp/webdata
echo "Hello from the host." > /tmp/webdata/host-hello.txt
```

### 🔹 Premier conteneur (PostgreSQL) :

```bash
docker run -it --name sql-database -v /tmp/webdata:/data postgres /bin/bash
```

Ajouter un fichier :

```bash
echo "Hello from SQL container." >> /data/sql-hello.txt
```

### 🔹 Deuxième conteneur (Apache + PHP) :

```bash
docker run -it --name webapp -v /tmp/webdata:/var/www/html php:5.6-apache /bin/bash
```

Ajouter un fichier :

```bash
echo "Hello from webapp container." >> /var/www/html/webapp-hello.txt
```

Vérification sur l’hôte :

```bash
ls /tmp/webdata
# host-hello.txt sql-hello.txt webapp-hello.txt
```

---

## 🧰 **7. Création de Bind Mount via `--mount`**

Alternative à `-v` :

```bash
docker run --mount type=bind,source=/var/app/data,target=/data my-container
```

Créer un bind mount persistant :

```bash
docker volume create \
  --driver local \
  -o o=bind \
  -o type=none \
  -o device=/var/app/data \
  example-volume
```

Et l’utiliser :

```bash
docker run -v example-volume:/data my-container
```

---

## 📦 **8. Conteneur comme volume de données partagé**

### 🔹 Étapes :

1. Créer le conteneur “volume de stockage” :
    
    ```bash
    docker run -it -v /shared-data --name data-storage centos /bin/bash
    ```
    
2. Ajouter un fichier :
    
    ```bash
    echo "Hello from data-storage" > /shared-data/data-storage-hello.txt
    ```
    
3. Lancer un conteneur Python partageant le volume :
    
    ```bash
    docker run -it --name app --volumes-from data-storage python /bin/bash
    ```
    
4. Vérifier :
    
    ```bash
    ls /shared-data
    # data-storage-hello.txt
    ```
    
5. Ajouter un fichier :
    
    ```bash
    echo "Hello from app container" > /shared-data/app-hello.txt
    ```
    
6. Lancer un conteneur Apache partageant le même volume :
    
    ```bash
    docker run -it --name web --volumes-from data-storage httpd /bin/bash
    ```
    
    Vérifier :
    
    ```bash
    ls /shared-data
    # app-hello.txt data-storage-hello.txt
    ```
    

---

## 🔒 **9. Volume en lecture seule (read-only)**

### 🔹 Étapes :

```bash
docker volume create --name limited-access
```

1. Conteneur avec écriture autorisée :
    
    ```bash
    docker run -it --name allowed-to-write -v limited-access:/data centos /bin/bash
    echo "Writable" > /data/hello.txt
    ```
    
2. Conteneur en lecture seule :
    
    ```bash
    docker run -it --name not-allowed-to-write -v limited-access:/data:ro centos /bin/bash
    echo "No write" > /data/no-access.txt
    # → bash: Read-only file system
    ```
    

---

## 🧹 **10. Nettoyage**

```bash
docker container stop $(docker ps -q)
docker container prune
docker volume prune
```

---

## ✅ **Résumé global**

|Méthode|Commande clé|Avantages|Limites|
|---|---|---|---|
|Volume nommé|`docker volume create`|Persistance, facile à partager|Pas de contrôle du chemin hôte|
|Bind mount|`-v /path:/path` ou `--mount`|Chemin précis sur l’hôte|Pas de nom, dépend du système|
|Dockerfile (VOLUME)|`VOLUME /dir`|Automatisable|Non configurable à l’exécution|
|Conteneur de données|`--volumes-from`|Partage entre conteneurs|Dépend du conteneur source|
|Lecture seule|`-v volume:/dir:ro`|Sécurise les accès|Non modifiable|

---

📘 **Source :**  
_Lab - 4 Docker Volumes (v22)_ — _Elies Jebri_  
🔗 Docs officielles : [https://docs.docker.com/storage/volumes/](https://docs.docker.com/storage/volumes/)

---

Souhaites-tu que je fasse une **fiche d’examen compacte (toutes les commandes essentielles)** pour ce lab aussi ?