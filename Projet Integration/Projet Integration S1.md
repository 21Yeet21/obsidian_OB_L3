
### **MPLS : Les VRF (Virtual Routing and Forwarding)**

- **Définition :**  
    Une **VRF** est une instance de routage virtuelle utilisée dans une infrastructure **MPLS** pour isoler plusieurs réseaux clients sur un même routeur physique.  
    Chaque VRF maintient sa propre table de routage, évitant toute interférence entre clients.
    
- **Principe :**
    
    - MPLS (Multiprotocol Label Switching) transporte les paquets à l’aide de **labels** au lieu d’adresses IP.
        
    - Chaque client ou service reçoit une **VRF distincte**, assurant la **séparation logique** du trafic.
        
    - Les paquets sont encapsulés avec un **label MPLS** qui identifie la VRF correspondante.
        
- **Avantages :**
    
    - Isolation totale du trafic (sécurité et confidentialité).
        
    - Mutualisation de l’infrastructure physique.
        
    - Simplification du déploiement de VPN (VPN MPLS).
        
- **Exemple concret :**  
    Un fournisseur d’accès Internet héberge plusieurs entreprises sur un même backbone MPLS — chaque entreprise dispose de sa propre VRF, donc ses routes et ses communications sont indépendantes.
    

---

### **VXLAN (VLAN étendu)**

- **Définition :**  
    **VXLAN** (Virtual eXtensible LAN) est une technologie d’encapsulation réseau permettant d’étendre un VLAN traditionnel sur plusieurs réseaux physiques ou virtuels.  
    Elle fonctionne sur **l’overlay network** (au-dessus de l’IP/UDP).
    
- **Principe :**
    
    - Chaque trame Ethernet est encapsulée dans un **tunnel UDP/IP**.
        
    - Les équipements appelés **VTEP (VXLAN Tunnel Endpoints)** réalisent cette encapsulation/décapsulation.
        
    - Identifiant VXLAN : **VNI (VXLAN Network Identifier)** — équivalent à un VLAN ID mais sur 24 bits (jusqu’à 16 millions de segments virtuels).
        
- **Avantages :**
    
    - Extension de VLANs à travers des réseaux L3 (pas limité au même switch ou au même LAN).
        
    - Idéal pour les **environnements virtualisés** et les **data centers**.
        
    - Meilleure **scalabilité** que les VLANs classiques (limités à 4096).
        
- **Exemple concret :**  
    Dans un cloud ou un data center multi-site, VXLAN permet de connecter des machines virtuelles sur des serveurs différents comme si elles étaient sur le même VLAN local.
    

---

### **Comparaison rapide :**

|Technologie|Couche|Objectif principal|Isolation|
|---|---|---|---|
|**MPLS/VRF**|L3|Séparer le routage entre clients|Par table de routage (VRF)|
|**VXLAN**|L2 (overlay sur L3)|Étendre un VLAN sur plusieurs sites|Par VNI (identifiant VXLAN)|

---

Souhaitez-vous que je reformule ce résumé dans un style **plus académique** adapté à ton rapport de projet (phrases continues, sans puces) ?