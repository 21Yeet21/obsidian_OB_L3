

---

## 🧱 **Objectif du lab**

Apprendre à **créer, gérer et optimiser des images Docker**, à la fois :

- à partir d’un **conteneur existant** ;
    
- via un **Dockerfile** ;
    
- et à comprendre la **structure des couches**, la **persistance**, et la **limitation des ressources**.
    

---

## ⚙️ **1. Création d’une image à partir d’un conteneur**

1. Lancer un conteneur Alpine :
    
    ```bash
    docker container run -it alpine ash
    ```
    
2. Installer un paquet (ex : figlet) :
    
    ```bash
    apk add figlet
    ```
    
3. Vérifier les changements :
    
    ```bash
    docker container diff <ID>
    ```
    
    → `A` (ajouté), `C` (modifié), `D` (supprimé)
    
4. Créer une image à partir du conteneur :
    
    ```bash
    docker container commit <ID>
    ```
    
5. Taguer l’image :
    
    ```bash
    docker image tag <ID> ourfiglet
    ```
    

💡 Résultat : une image personnalisée nommée `ourfiglet` basée sur Alpine.

---

## 🧾 **2. Création d’image via un Dockerfile**

### Exemple Node.js “Hello World”

```dockerfile
FROM alpine
RUN apk update && apk add nodejs
COPY . /app
WORKDIR /app
CMD ["node", "index.js"]
```

**Étapes :**

1. Créer `index.js` :
    
    ```js
    var os = require("os");
    console.log("hello from " + os.hostname());
    ```
    
2. Construire l’image :
    
    ```bash
    docker image build -t hello:v0.1 .
    ```
    
3. Lancer le conteneur :
    
    ```bash
    docker container run hello:v0.1
    ```
    

---

## 🧩 **3. Couches d’images (Layers)**

Chaque **instruction du Dockerfile crée une couche** :

- `FROM` → couche de base
    
- `RUN` → ajout de dépendances
    
- `COPY` → ajout du code
    

Lister les couches :

```bash
docker image history <IMAGE_ID>
```

💡 Lors d’une modification (ex : `index.js` mis à jour en `v0.2`),  
Docker **réutilise les couches en cache** si rien n’a changé → gain de temps et d’espace.

---

## 🔍 **4. Inspection d’images**

Afficher toutes les infos :

```bash
docker image inspect alpine
```

Afficher uniquement les couches :

```bash
docker image inspect --format "{{ json .RootFS.Layers }}" hello:v0.2
```

→ On peut voir que plusieurs images partagent les **mêmes couches de base**.

---

## 🌐 **5. Exemple complet avec NGINX**

### Structure :

```
nginx/
├── Dockerfile
└── files/
    ├── nginx.conf
    ├── default.conf
    └── html.tar.gz
```

### Dockerfile :

```dockerfile
FROM alpine:latest
LABEL maintainer="Elies Jebri <elies.jebri@gmail.com>"
RUN apk add --update nginx && rm -rf /var/cache/apk/* && mkdir -p /tmp/nginx/
COPY files/nginx.conf /etc/nginx/nginx.conf
COPY files/default.conf /etc/nginx/conf.d/default.conf
ADD files/html.tar.gz /usr/share/nginx/
EXPOSE 80/tcp
ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]
```

### Construction et exécution :

```bash
docker image build -t eliesjebri/mynginx:1.0 .
docker container run -d -p 8080:80 --name mynginx1 eliesjebri/mynginx:1.0
```

→ Accès via `http://localhost:8080` → page "Hello world! This is being served from Docker."

---

## 🧭 **6. ENTRYPOINT vs CMD**

- `ENTRYPOINT` définit le **binaire principal** (ex : `nginx`)
    
- `CMD` définit les **arguments par défaut**
    

Exemple :

```bash
docker run mynginx -v
```

→ équivaut à `nginx -v`

---

## ⚡ **7. Limitation des ressources**

Par défaut, un conteneur peut utiliser **toutes les ressources** de l’hôte.

### Mise à jour des limites :

```bash
docker container update --cpu-shares 512 --memory 128M --memory-swap 256M nginx-test
```

### Au lancement :

```bash
docker run -d --name nginx-test --cpu-shares 512 --memory 128M -p 8081:80 nginx
```

---

## 🧹 **8. Nettoyage des conteneurs**

Lister tous les conteneurs :

```bash
docker container ls -aq
```

Arrêter et supprimer :

```bash
docker container stop $(docker container ls -aq)
docker container rm $(docker container ls -aq)
```

Supprimer les conteneurs arrêtés :

```bash
docker container prune
```

---

## ✅ **Résumé général**

|Concept|Commande principale|Résultat|
|---|---|---|
|Créer une image depuis conteneur|`docker commit`|Image locale|
|Créer via Dockerfile|`docker build`|Image versionnée|
|Exécuter conteneur|`docker run`|Application lancée|
|Voir les couches|`docker history`|Structure de l’image|
|Inspecter image|`docker inspect`|Détails JSON|
|Limiter ressources|`docker run --memory`|Conteneur isolé|
|Nettoyer conteneurs|`docker prune`|Espace libéré|

---

📘 **Source :**  
**Lab – Docker Images (v24)** – _Elies Jebri_  
Documentation officielle : [https://docs.docker.com](https://docs.docker.com)

---

Souhaitez-tu que je te crée aussi une **fiche pratique de commandes Docker** (avec explication courte + exemple) pour ce même lab ?