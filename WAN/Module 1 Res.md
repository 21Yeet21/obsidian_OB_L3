
---

# 🧭 Chapitre 1 – Concepts WAN (Résumé Complet + Guide visuel)

---

## 🎯 1️⃣ But & idée générale

- Le **WAN (Wide Area Network)** connecte plusieurs **LAN géographiquement distants**.
    
- Il est fourni et maintenu par un **fournisseur de services (FAI / opérateur)**.
    
- Permet :
    
    - La communication entre succursales d’une entreprise.
        
    - L’accès à Internet pour les réseaux privés.
        
    - L’interconnexion de sites distants via technologies publiques ou privées.
        

---

## 🏛️ 2️⃣ WAN privé vs WAN public

|Type|Description|Exemple|
|---|---|---|
|**Privé**|Ligne louée ou VPN d’entreprise dédié. Sécurité et QoS garanties.|MPLS, Fibre dédiée|
|**Public**|Passe par Internet. Moins cher, mais partagé et sans SLA.|VPN IPsec, SD-WAN|

---

## 🧩 3️⃣ Différence LAN vs WAN

**À voir :** _Diapo 12 environ_  
**Image à chercher :** schéma comparant un petit LAN (switch + PCs) et un WAN reliant plusieurs LANs via un nuage (“cloud”).  
**À retenir :**

- LAN = propriété de l’entreprise, rapide (Gbps).
    
- WAN = service externe, longue distance, coût élevé.
    

---

## 🔗 4️⃣ Topologies WAN (logiques)

**À voir :** _Diapos 14 → 19_

### a) Point-à-Point

- Liaison directe entre deux sites.
    
- Simple mais coûteuse à grande échelle.  
    **Image :** 2 routeurs reliés par une seule ligne.
    

### b) Hub-and-Spoke (Étoile)

- Un site central relie toutes les succursales.
    
- Si le hub tombe, tout s’arrête.  
    **Image :** 1 routeur central + 4 branches.
    

### c) Dual-Homed

- Chaque succursale a deux liaisons vers le fournisseur.
    
- Tolérance aux pannes.  
    **Image :** même étoile mais chaque spoke relié à 2 hubs.
    

### d) Maillage partiel / complet

- **Complet** : chaque site parle à tous. → Redondant, coûteux.
    
- **Partiel** : certains liens directs. → Équilibre coût/performance.  
    **Image :** 4–5 routeurs reliés par plusieurs lignes croisées.
    

---

## ⚙️ 5️⃣ Terminologie importante

| Terme                    | Signification                                          | Exemple               |
| ------------------------ | ------------------------------------------------------ | --------------------- |
| **DTE**                  | Data Terminal Equipment = équipement client (routeur). | Routeur Cisco         |
| **DCE**                  | Data Communications Equipment = équipement du FAI.     | Modem, CSU/DSU        |
| **Boucle locale**        | Liaison physique entre client et central téléphonique. | Cuivre ADSL / Fibre   |
| **Point de démarcation** | Limite entre réseau client et FAI.                     | Prise murale, NT1     |
| **Serveur d’accès**      | Authentifie les connexions distantes.                  | RADIUS, NAS           |
| **DSLAM**                | Agrège connexions DSL côté fournisseur.                | Tunisie Télécom DSLAM |

---

## 🧱 6️⃣ Périphériques WAN courants

**Image :** _Diapo ~22_  
Représente : Modem, CSU/DSU, Routeur, DSLAM, Satellite CPE.  
**Rôle :** conversion, multiplexage, accès et terminaison.

---

## 🔄 7️⃣ Commutation (Switching)

|Type|Fonctionnement|Exemple|
|---|---|---|
|**Message**|Stocke → transmet tout le message ; obsolète.|Télégraphie|
|**Circuit**|Circuit dédié pendant toute la session.|RTC, ISDN|
|**Paquet**|Découpe les données ; paquets indépendants.|Internet, MPLS|

---

## 🧬 8️⃣ Couches OSI & Protocoles WAN

**À voir :** _Diapo 28 environ_  
**Image :** tableau associant couches 1/2 aux technologies.

|Couche|Technologies|
|---|---|
|**L1 – Physique**|SDH, SONET, DWDM|
|**L2 – Liaison**|PPP, HDLC, Frame Relay, ATM, MPLS, Ethernet WAN|

---

## 💡 9️⃣ Technologies physiques / Multiplexage

**À voir :** _Diapo 35 environ_  
**Image :** fibres optiques + flèches colorées λ1, λ2 (DWDM).  
**À retenir :**

- **SDH/SONET :** transport synchrone sur fibre.
    
- **DWDM :** multiplexage de longueurs d’onde → haut débit.
    

---

## 🧭 10️⃣ WAN traditionnels vs modernes

**À voir :** _Diapos 45 → 47_

### a) Technos anciennes

- **Lignes louées (T1/E1, T3/E3)** : fiables, mais chères.
    
- **Frame Relay, ATM** : paquets virtuels, remplacés.
    

### b) Technos modernes

- **Metro Ethernet / EoMPLS :** Ethernet étendu via opérateur.
    
- **MPLS :** routage via labels, QoS garantie.  
    **Image :** nuage “Provider MPLS” avec routeurs P/PE reliés aux clients.
    

---

## 🌐 11️⃣ Connectivité basée sur Internet

**À voir :** _Diapo 52 environ_  
**Image :** modem ADSL, routeur client, DSLAM et PPPoE.  
**Technos :**

- **Filaire :** DSL, Câble (DOCSIS), Fibre (FTTH/FTTB/FTTN).
    
- **Sans fil :** 3G/4G/5G, WiMAX, Satellite.
    
- **VPN :** chiffrement + authentification.
    

---

## 🔐 12️⃣ VPN et connectivité sécurisée

**À voir :** _Diapo 55 environ_  
**Image :** deux sites reliés par un tunnel chiffré dans le nuage Internet.  
**À retenir :**

- **Site-à-site :** entre 2 routeurs d’entreprises.
    
- **Accès distant :** utilisateur → réseau de l’entreprise.
    
- Protocoles : IPsec, SSL, GRE.
    

---

## ⚡ 13️⃣ Avantages / Limites des solutions haut débit

|Technologie|Avantages|Limites|
|---|---|---|
|**Câble**|Haut débit partagé|Contention aux heures de pointe|
|**DSL**|Bon coût, facile|Distance ↔ central limite le débit|
|**Fibre**|Très haut débit|Coût d’installation|
|**4G/5G/Satellite**|Mobilité|Latence, fiabilité variable|

---

## 🧠 14️⃣ Mnémotechniques rapides

- **“SDH SONeT DWDM = Fibre Power”** → Couche 1.
    
- **“PPP HDLC FR ATM ETH MPLS = Link Layer”** → Couche 2.
    

---

## 📝 15️⃣ Quiz de révision

1. Donner 2 différences entre WAN privé et public.
    
2. Citer 3 types de commutation avec exemples.
    
3. Expliquer MPLS en 1 phrase.
    
4. Citer 2 technologies modernes utilisées en Tunisie Télécom.
    

---

## 🧩 16️⃣ Résumé final

- **WAN = interconnexion de LAN distants.**
    
- **Technologies modernes :** MPLS, Ethernet WAN, SD-WAN.
    
- **Couche 1 :** SONET, SDH, DWDM.
    
- **Couche 2 :** PPP, Frame Relay, ATM, MPLS.
    
- **Accès :** DSL, Câble, Fibre, 4G/5G, Satellite.
    
- **VPN :** sécurité + chiffrement + interconnexion d’entreprises.
    

---

### 🗺️ Récapitulatif des diapositives à chercher dans ton PDF

|Section|Sujet principal|Diapo approximative|
|---|---|---|
|LAN vs WAN|Différences conceptuelles|~12|
|Topologies WAN|P2P, Hub-Spoke, Mesh|14–19|
|OSI & protocoles WAN|Couches 1–2|~28|
|Multiplexage DWDM|Fibre optique|~35|
|MPLS / Ethernet WAN|Modernisation du WAN|45–47|
|DSL / PPPoE / DSLAM|Boucle locale|~52|
|VPN & Tunnels|Sécurité|~55|

---

Would you like me to continue with **Chapitre 2 – Fonctionnement du WAN** (same style : explanations + visual map + slide numbers)?