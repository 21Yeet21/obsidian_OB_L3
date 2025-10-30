
---

## 🧾 **DEVOIR — Introduction à l’IoT**

### **Q1.** Quels sont les domaines d'application pour lesquels on a vu des systèmes IoT se développer ? Donner un exemple d'application par domaine.

**Réponse :**  
Les principaux domaines d’application de l’IoT sont :

- **Ville intelligente (Smart City)** : gestion du trafic, éclairage public, collecte des déchets.  
    → _Exemple : capteurs de stationnement pour optimiser la circulation._
    
- **Santé (e-Health)** : suivi à distance des patients.  
    → _Exemple : montres connectées mesurant la fréquence cardiaque._
    
- **Agriculture intelligente (Smart Farming)** : irrigation et surveillance des cultures.  
    → _Exemple : capteurs d’humidité du sol pour automatiser l’arrosage._
    
- **Industrie (IIoT)** : maintenance prédictive et contrôle à distance.  
    → _Exemple : capteurs de vibration sur machines industrielles._
    
- **Environnement** : détection de pollution, incendies, séismes.  
    → _Exemple : capteurs de CO₂ pour surveiller la qualité de l’air._
    
- **Domotique** : automatisation des habitations.  
    → _Exemple : contrôle d’éclairage et de chauffage via smartphone._
    

---

### **Q2.** Quelles sont les fonctions qui doivent être assurées par un système IoT ? Donner une brève définition pour chacune.

**Réponse :**

1. **Détection (Sensing)** — Les capteurs collectent les données physiques.
    
2. **Communication (Networking)** — Transmission des données vers un autre appareil ou vers le cloud.
    
3. **Traitement (Processing)** — Analyse, filtrage ou prise de décision à partir des données.
    
4. **Action (Actuation)** — Les actionneurs exécutent une commande (ouverture, alarme, etc.).
    
5. **Stockage & Visualisation** — Les données sont conservées et affichées à l’utilisateur.
    

---

### **Q3.** Se référant aux briques fonctionnelles de l’IoT, donner l’architecture en couche d'une plateforme IoT. Énumérer les fonctions assurées par chaque couche.

**Réponse :**

1. **Couche de perception** : capteurs et actionneurs qui détectent et transmettent les informations du monde réel.
    
2. **Couche réseau (transport)** : assure la communication des données vers la plateforme (Wi-Fi, 4G, ZigBee…).
    
3. **Couche application** : analyse, stockage et interface utilisateur pour exploiter les données.
    

---

### **Q4.** Définir un objet connecté.

**Réponse :**  
Un **objet connecté** est un dispositif capable de **collecter, transmettre ou recevoir des données via Internet ou un autre réseau** afin d’interagir avec son environnement ou d’autres objets sans intervention humaine directe.

---

### **Q5.** Proposer une classification pour les réseaux d'accès pour l'IoT en donnant un exemple pour chaque type.

**Réponse :**

1. **Short Range (courte portée)** : Wi-Fi, Bluetooth, ZigBee, NFC.
    
2. **Wide Range (longue portée)** : 4G, 5G, LoRa, Sigfox, NB-IoT.
    
3. **Mixed Range (mixte)** : combinaison de technologies (ex. : capteur BLE → passerelle 4G).
    

---

### **Q6.** Quels sont les menaces auxquels sont soumis les réseaux d'accès pour l'IoT ?

**Réponse :**

- Interception de données (écoute, sniffing).
    
- Usurpation d’identité ou spoofing.
    
- Attaques DoS/DDoS (saturation du réseau).
    
- Injections de malwares ou ransomwares.
    
- Failles d’authentification (mots de passe faibles).
    
- Vol ou perte d’intégrité des données.
    

---

## 📘 **EXAMEN — Janvier 2021**

### **Q1.** Expliquer brièvement le rôle de chaque couche du modèle d’architecture IoT suivant :

- **Application layer**
    
- **Service and Application support layer**
    
- **Network layer**
    
- **Device layer**
    

**Réponse :**

- **Application layer :** fournit les applications IoT destinées à l’utilisateur final (santé, transport, ville intelligente).
    
- **Service and Application Support layer :** offre des services de stockage, sécurité, gestion et traitement des données.
    
- **Network layer :** gère la connectivité, l’adressage IP, le transport des données (Wi-Fi, LTE, LoRa…).
    
- **Device layer :** composée de capteurs, actionneurs et passerelles qui collectent et transmettent les données.
    

---

### **Q2.** Expliquer la différence entre les deux architectures des systèmes IoT de collecte de données short range et mixed.

**Réponse :**

- **Short Range :** communication directe entre objets (Bluetooth, ZigBee). → portée limitée, consommation faible.
    
- **Mixed Range :** combinaison d’un réseau local court (BLE, ZigBee) avec un réseau longue portée (4G, Wi-Fi) via une passerelle. → permet la communication avec le cloud.
    

---

