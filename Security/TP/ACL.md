
### **Partie Théorique : Les Listes de Contrôle d’Accès Standard (ACL Standard)**

Les listes de contrôle d’accès (ACL) sont des mécanismes de sécurité utilisés sur les routeurs et commutateurs pour filtrer le trafic réseau. Elles permettent de contrôler quels paquets IP sont autorisés ou refusés à travers une interface selon des critères définis par l’administrateur.

Une **ACL standard** agit uniquement sur l’adresse IP source des paquets. Elle ne prend pas en compte les ports, les protocoles ou les adresses de destination. Son rôle principal est de **permettre ou bloquer le trafic provenant d’un hôte ou d’un réseau spécifique**.

Les ACL standard sont numérotées de **1 à 99** (ou de **1300 à 1999** pour les ACL étendues numérotées).  
Elles doivent être placées **le plus près possible de la destination** pour éviter de bloquer inutilement d’autres flux légitimes.

#### **Fonctionnement**

- Le routeur examine chaque paquet entrant sur l’interface où l’ACL est appliquée.
    
- Les conditions sont évaluées de haut en bas, dans l’ordre des lignes configurées.
    
- Dès qu’un paquet correspond à une condition, l’action (permit ou deny) est exécutée.
    
- S’il ne correspond à aucune condition, il est automatiquement **refusé** (implicite _deny all_ à la fin de chaque ACL).
    

#### **Syntaxe de base**

```bash
Router(config)# access-list <numéro> {permit | deny} <source> <wildcard-mask>
Router(config-if)# ip access-group <numéro> {in | out}
```

#### **Exemple**

```bash
Router(config)# access-list 10 deny 192.168.1.10
Router(config)# access-list 10 permit any
Router(config-if)# ip access-group 10 in
```

Dans cet exemple, tout trafic provenant de l’adresse 192.168.1.10 est bloqué, tandis que les autres adresses sont autorisées.

#### **Bonnes pratiques**

- Utiliser des descriptions claires pour faciliter la maintenance.
    
- Tester les ACL sur un environnement de simulation avant leur mise en production.
    
- Documenter chaque règle pour comprendre l’objectif du filtrage.
    

---
Voici la **partie théorique** complète que tu peux directement insérer dans ton **compte rendu** pour le chapitre **ACL étendue (Extended ACL)** :

---

### **Partie Théorique : Les Listes de Contrôle d’Accès Étendues (ACL Étendues)**

Les **ACL étendues** sont une version avancée des listes de contrôle d’accès permettant de filtrer le trafic réseau de manière plus précise que les ACL standard.  
Elles offrent un **contrôle granulaire** sur le trafic IP en se basant non seulement sur l’adresse source, mais aussi sur **l’adresse de destination, le protocole, et les ports** utilisés.

Contrairement aux ACL standard, les ACL étendues permettent donc de **définir des politiques de sécurité plus fines**, adaptées à des besoins spécifiques (ex. : autoriser le HTTP, bloquer le Telnet, etc.).

#### **Plage de numérotation**

Les ACL étendues utilisent les numéros :

- **100 à 199**
    
- **2000 à 2699** (plage étendue)
    

#### **Fonctionnement**

- Chaque ligne d’une ACL est évaluée séquentiellement, du haut vers le bas.
    
- Le routeur compare le trafic réseau avec les critères de l’ACL :
    
    - Adresse IP source
        
    - Adresse IP de destination
        
    - Protocole (TCP, UDP, ICMP, IP)
        
    - Numéro de port (ex : 80 pour HTTP, 23 pour Telnet, etc.)
        
- Dès qu’une condition est satisfaite, l’action (permit ou deny) est appliquée.
    
- Un **deny implicite** est présent à la fin de chaque ACL.
    

#### **Syntaxe de base**

```bash
Router(config)# access-list <numéro> {permit | deny} <protocole> <source> <wildcard> <destination> <wildcard> [opérateur port]
Router(config-if)# ip access-group <numéro> {in | out}
```

#### **Exemples**

1. **Autoriser le trafic HTTP du LAN 192.168.1.0 vers un serveur web 10.10.10.10**
    
    ```bash
    Router(config)# access-list 101 permit tcp 192.168.1.0 0.0.0.255 10.10.10.10 0.0.0.0 eq 80
    ```
    
2. **Bloquer tout le trafic ICMP (ping) vers le réseau 172.16.0.0/16**
    
    ```bash
    Router(config)# access-list 101 deny icmp any 172.16.0.0 0.0.255.255
    ```
    
3. **Autoriser tout autre trafic**
    
    ```bash
    Router(config)# access-list 101 permit ip any any
    Router(config-if)# ip access-group 101 in
    ```
    

#### **Emplacement recommandé**

Les ACL étendues doivent être placées **le plus près possible de la source** du trafic, afin de limiter le flux indésirable avant qu’il ne traverse tout le réseau.

#### **Bonnes pratiques**

- Nommer les ACL pour faciliter la gestion et la lecture :
    
    ```bash
    Router(config)# ip access-list extended NOM_ACL
    ```
    
- Documenter chaque règle avec des commentaires clairs.
    
- Éviter de bloquer le trafic essentiel (DNS, DHCP, etc.).
    
- Tester la configuration avant le déploiement en production.
    

---

