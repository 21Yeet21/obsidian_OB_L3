Here’s a **complete and clear summary** of your **Lab – Docker ENV (v23)** by _Elies Jebri_ 👇

---

## 🧱 **Objectif du lab**

Découvrir et utiliser les **variables d’environnement (ENV)** dans Docker pour :

- configurer des images et conteneurs dynamiques,
    
- personnaliser l’exécution d’applications,
    
- et automatiser la configuration (Apache, PHP, MySQL).
    

---

## ⚙️ **1. Variables d’environnement dans un Dockerfile**

### 🔹 Syntaxe :

```dockerfile
ENV <key> <value>
```

Exemple :

```dockerfile
ENV username admin
```

---

### 🔹 Exemple pratique : image Apache + PHP

#### Dockerfile :

```dockerfile
FROM alpine:3.16
LABEL maintainer="Elies Jebri <elies.jebri@gmail.com>"
LABEL description="Cet exemple installe Apache & PHP."
ARG PHPVERSION
RUN apk add --update apache2 php${PHPVERSION}-apache2 php${PHPVERSION} && \
    rm -rf /var/cache/apk/* && \
    rm -rf /var/www/localhost/htdocs/index.html && \
    echo "<?php phpinfo(); ?>" > /var/www/localhost/htdocs/index.php && \
    chmod 755 /var/www/localhost/htdocs/index.php
EXPOSE 80/tcp
ENTRYPOINT ["httpd"]
CMD ["-D", "FOREGROUND"]
```

**Construction de l’image :**

```bash
docker build -t local/apache-php:8 --build-arg PHPVERSION=8 .
```

**Exécution du conteneur :**

```bash
docker run -d -p 8080:80 --name apache-php8 local/apache-php:8
```

➡️ Page disponible sur **[http://localhost:8080](http://localhost:8080)**

---

## 🌍 **2. Passer des variables à l’exécution**

Les variables peuvent être définies **au lancement d’un conteneur** avec `--env` (`-e`).

### 🔹 Exemple 1 – Valeur directe :

```bash
docker run --env VARIABLE1=foobar alpine env
```

### 🔹 Exemple 2 – Variable d’environnement locale :

```bash
export VARIABLE2=foobar2
docker run --env VARIABLE2 alpine env
```

### 🔹 Exemple 3 – Variable inline :

```bash
VARIABLE3=foobar3 docker run --env VARIABLE3 alpine env
```

---

### 🔹 Exemple 4 – Fichier `.env`

Créer un fichier `my-env.txt` :

```bash
echo VARIABLE1=foobar1 > my-env.txt
echo VARIABLE2=foobar2 >> my-env.txt
echo VARIABLE3=foobar3 >> my-env.txt
```

Puis :

```bash
docker run --env-file my-env.txt alpine env
```

---

## 🧾 **3. Utiliser ENV pour personnaliser une page PHP**

Créer un script d’entrée (`message-entrypoint.sh`) pour générer une page dynamique à partir d’une variable `MESSAGE`.

### 🔹 Dockerfile-message :

```dockerfile
FROM local/apache-php:8
LABEL maintainer="Elies Jebri <elies.jebri@gmail.com>"
COPY message-entrypoint.sh /bin
RUN chmod 555 /bin/message-entrypoint.sh && \
    rm -rf /var/www/localhost/htdocs/index.html
EXPOSE 80/tcp
ENTRYPOINT ["/bin/message-entrypoint.sh"]
```

### 🔹 Script `message-entrypoint.sh` :

```bash
#!/bin/sh
echo "<?php echo '<p>$MESSAGE</p>'; ?>" > /var/www/localhost/htdocs/index.php
chmod 755 /var/www/localhost/htdocs/index.php
httpd -D FOREGROUND
```

### 🔹 Construction & exécution :

```bash
docker build -f Dockerfile-message -t local/php-message .
docker run -d -p 8080:80 -e MESSAGE=Hello --name message-hello local/php-message
```

Résultat :

```bash
curl http://localhost:8080
<p>Hello</p>
```

---

## 🗄️ **4. Gestion d’un conteneur MySQL**

### 🔹 Premier essai :

```bash
docker run --name mysql-db mysql:5.7
```

❌ Erreur : variables obligatoires manquantes (`MYSQL_ROOT_PASSWORD`, etc.)

---

### 🔹 Relancer avec les variables requises :

```bash
docker run -d --name mysql-db \
 -e MYSQL_USER=user1 \
 -e MYSQL_PASSWORD=password \
 -e MYSQL_DATABASE=items \
 -e MYSQL_ROOT_PASSWORD=password \
 mysql:5.7
```

Vérifier :

```bash
docker ps
```

---

### 🔹 Inspection du conteneur :

```bash
docker inspect -f '{{ .Path }} {{ .NetworkSettings.IPAddress }}' mysql-db
# Résultat exemple : docker-entrypoint.sh 172.17.0.2
```

---

### 🔹 Connexion depuis l’hôte :

```bash
yum install mysql
mysql -u user1 -h 172.17.0.2 -p items
```

Créer une table :

```sql
CREATE TABLE Projects (
  id int(11) NOT NULL,
  name varchar(255),
  code varchar(255),
  PRIMARY KEY (id)
);
INSERT INTO Projects VALUES (1,'DevOps','DO701');
SELECT * FROM Projects;
```

---

### 🔹 Vérifier la persistance (volume) :

```bash
docker inspect -f '{{ range .Mounts }}{{ .Source }}<-:->{{ .Destination }} {{ end }}' mysql-db
```

➡️ Exemple :

```
/var/lib/docker/volumes/.../_data <-:-> /var/lib/mysql
```

- Le dossier `/var/lib/mysql` dans le conteneur est stocké sur le volume de l’hôte.
    
- Cela assure la **persistance des données** même après suppression du conteneur.
    

---

### 🔹 Sauvegarde et suppression :

```bash
mkdir mysql-db && cd mysql-db
cp -Rp /var/lib/docker/volumes/.../_data .
docker stop mysql-db
docker rm mysql-db
```

---

## ✅ **Résumé général**

|Objectif|Commande principale|Résultat|
|---|---|---|
|Définir une variable dans Dockerfile|`ENV key value`|Variable permanente dans l’image|
|Passer une variable à l’exécution|`docker run -e VAR=value`|Variable disponible dans le conteneur|
|Utiliser fichier `.env`|`docker run --env-file my-env.txt`|Injection multiple de variables|
|Personnaliser avec script d’entrée|`ENTRYPOINT` + `$MESSAGE`|Page dynamique|
|Créer conteneur MySQL configuré|`-e MYSQL_USER=...` etc.|Base de données initialisée|
|Voir volume persistant|`docker inspect -f '{{ .Mounts }}'`|Emplacement des données MySQL|

---

📘 **Source :**  
_Lab - 2 Docker ENV (v23)_ — _Elies Jebri_  
🔗 Documentation officielle : [https://docs.docker.com/engine/reference/run/#env-environment-variables](https://docs.docker.com/engine/reference/run/#env-environment-variables)

---

Souhaites-tu que je fasse maintenant une **fiche pratique (résumée en commandes uniquement)** pour ce lab, comme un _aide-mémoire d’examen_ ?