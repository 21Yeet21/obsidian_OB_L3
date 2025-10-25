
### **Trame HDLC : II | SS | UN**

- **II (Information Frame)**
    
    - Sert à transporter les données utilisateur.
        
    - Contient aussi le numéro de séquence pour assurer le contrôle d’erreurs et le suivi des trames.
        
- **SS (Supervision Frame)**  
    Sert à contrôler le flux et la correction des erreurs. Elle se divise en 4 types selon les bits de contrôle :
    
    - **00 : RR (Receive Ready)** → **ACK** (l’émetteur peut continuer à envoyer).
        
    - **01 : RNR (Receive Not Ready)** → **ACK mais Stop** (le récepteur est occupé, il demande une pause).
        
    - **10 : REJ (Reject)** → **NACK global** (demande de retransmettre plusieurs trames depuis l’erreur).
        
    - **11 : SREJ (Selective Reject)** → **NACK sélectif** (demande la retransmission d’une seule trame spécifique).
        
- **UN (Unnumbered Frame)**
    
    - Utilisée pour des fonctions de **gestion** et de **contrôle de la liaison** (ex. établissement, libération de connexion, tests).
        
    - Ne transporte pas de données utilisateur.
        

---

👉 En résumé :

- **II** = données.
    
- **SS** = contrôle du flux / erreurs avec ACK ou NACK.
    
- **UN** = gestion de la liaison.
    

