Great — we’ll go deep on **MPLS** and stop right where the deck reaches **VPN MPLS (couche 3)** (around slide 41).  
I’ll give an exam-focused, Obsidian-ready summary (organized, compact), **plus precise image descriptions and slide numbers** so you can find and screenshot the exact diagrams to paste into your notes. Where I refer to the course PDF content I’ll cite it.

### Plan

- Quick conceptual overview
    
- Data plane: label header & operations (push / swap / pop)
    
- Control plane: how labels are distributed (LDP, RSVP, BGP)
    
- Key concepts: FEC, LSP, LSR, PE/CE, label stacking, EXP/TTL
    
- Services enabled by MPLS up to **VPN couche-3** (RFC 2547 ideas, VRF) — stop there
    
- Images to screenshot (slide references) + short exam drill
    

---

### ### Qu’est-ce que MPLS — idée simple

- **MPLS = Multiprotocol Label Switching** : mécanisme d’encapsulation où on ajoute une **étiquette (label)** devant le paquet IP (ou une trame L2) pour acheminer rapidement sans regarder l’en-tête IP à chaque saut.
    
- Buts : accélérer le forwarding, permettre des services (VPN, ingénierie du trafic, pseudowires) et offrir QoS.
    

---

### ### En-tête de label (format essentiel)

- Structure (32 bits) :
    
    - **Label** (20 bits)
        
    - **EXP / CoS** (3 bits) pour la priorité / QoS
        
    - **S** (1 bit) : bottom-of-stack
        
    - **TTL** (8 bits)
        
- Connaître ces champs = question d’examen fréquente.
    

**Image à capturer** : schéma de l’en-tête d’étiquette (page ~10–11). Cherche le diagramme montrant Label/EXP/S/TTL.

---

### ### Opérations sur les labels (Data plane)

- **Push (imposer)** : le PE d’entrée impose une ou plusieurs étiquettes au paquet (ex. entrée d’un VPN).
    
- **Swap (échanger)** : chaque LSR intermédiaire remplace l’étiquette entrante par l’étiquette de sortie (très rapide).
    
- **Pop (retirer)** : le PE de sortie ou le LSR avant sortie enlève l’étiquette et remet le paquet IP « nu » pour routage final.
    
- **Penultimate Hop Popping (PHP)** : optimisation où l’avant-dernier LSR dépile pour réduire le travail du PE de sortie.
    

**Image à capturer** : flux « entrée → swap → sortie » (slides ~14–16 montrant fonctionnement et étapes).

---

### ### FEC, LSP, LSR, PE, CE — définitions pratiques

- **FEC (Forwarding Equivalence Class)** : groupe de paquets traités de la même façon (mappés sur un même LSP).
    
- **LSP (Label Switched Path)** : chemin établi dans le cœur MPLS pour les paquets d’une FEC.
    
- **LSR (Label Switch Router)** : routeur du cœur qui swappe les labels.
    
- **PE (Provider Edge)** : routeur bordure du fournisseur qui impose / retire labels et gère VRF.
    
- **CE (Customer Edge)** : équipement client connecté au PE.
    

**Image à capturer** : schéma FEC → LSP → LSR / PE / CE (slides ~13–15).

---

### ### Distribution des labels (Control plane)

- **LDP (Label Distribution Protocol)** : protocole de base (RFC) pour distribuer des labels pour des FEC annoncées par IGP/IGP-routes. Supporte découverte de voisins et échange d’étiquettes. (slides ~25–27).
    
- **RSVP-TE** : protocole utilisé pour **Traffic Engineering** — permet d’établir LSPs avec réservation de bande passante et routes explicites (PATH/RESV messages). (slides ~28).
    
- **BGP (MP-BGP)** : utilisé pour distribuer les routes et labels dans le contexte **VPN MPLS** (VPNv4, échanges d’étiquettes via iBGP entre PE). (slides ~29–31, 41).
    

**Image à capturer** : LDP neighbor discovery / LDP exchange (slide ~25) et RSVP PATH/RESV concept (slide ~28).

---

### ### Allocation & échange d’étiquettes — flux logique

- Mode courant : **downstream unsolicited** (un LSR propose une étiquette pour une FEC à ses voisins — allocation « aval »).
    
- Exemple d’assignation : tableau montrant préfixe → interface de sortie → label de sortie (slides ~20–25). Comprends comment un LSR mappe préfixe → label.
    

**Image à capturer** : exemple de table d’attribution de labels (slides ~21–24).

---

### ### Pile d’étiquettes (Label stacking)

- Plusieurs labels peuvent être empilés : utile pour TE, VPNs (outer label pour transport LSP, inner label pour identifier le VPN/FEC).
    
- **S bit** indique le label en bas de pile.
    

**Image à capturer** : schéma de pile d’étiquettes montrant étiquettes internes/externes et EOS bit (slides ~30–31).

---

### ### Services rendus possibles (jusqu’à VPN L3)

- **VPN L2 (AToM, pseudowires)** : émulé via étiquettes, transporte trames L2 sur LSP. (slides ~50–54 — note, beyond our stop but keep aware).
    
- **VPN L3 (BGP/MPLS VPN — RFC 2547 style)** : le fournisseur instancie des **VRF (Virtual Routing and Forwarding)** par client, échange des routes VPN via **MP-BGP** et distribue labels pour ces routes. Le PE d’entrée impose **2 étiquettes** souvent : une interne (VPN) et une externe (transport). (slides ~34–41).
    

**Image à capturer** : architecture VPN L3 (PE/CE, VRF, iBGP VPNv4 exchange) — slides ~34–41. Ces pages sont cruciales.

---

### ### Pourquoi MPLS + VPN L3 marche (concept clé)

- Le PE maintient une **table VRF** pour chaque VPN — sépare les tables de routage.
    
- **MP-BGP** transporte des routes VPNv4 (préfixe + RD) et les labels associés.
    
- Le PE d’entrée impose une étiquette VPN (pour identifier la VRF) puis l’étiquette IGP/MPLS pour transporter à travers le backbone. À la sortie, le PE dépile et remet le paquet dans la table VRF correcte.
    

**Image à capturer** : diagramme montrant entrée PE imposant 2 labels et sortie PE dépilant (slide ~44 shows imposing 2 labels — capture slides ~41–44).

---

### ### Ingénierie du trafic (MPLS-TE) — brève introduction (relevant but deeper later)

- MPLS-TE permet d’établir LSPs explicites avec réservation de bande passante via RSVP-TE.
    
- Utile pour contourner congestion et construire VLL (virtual leased line) garanties. (slides ~55–66).
    

**Image à capturer (optional)** : schéma montrant TE tunnels primaires/secondaires et protection FRR (slides ~62–64).

---

### ### Commandes & vérifications (rapide)

- activer CEF, activer MPLS sur l’interface :
    
    - `ip cef`
        
    - `interface X` → `mpls ip`
        
    - activer LDP : `mpls label protocol ldp`
        
- commandes show utiles : `show mpls ldp discovery`, `show mpls ip binding`, `show mpls forwarding-table`. (slides ~66–68).
    

---

### ### Exam focus — ce que tombera sûrement

- Savoir dessiner/un expliquer : **push/swap/pop** et le rôle du PE/LSR/CE.
    
- Connaître la **structure de l’en-tête** label (20/3/1/8).
    
- Expliquer comment **VPN L3** utilise VRF + MP-BGP + labels (RFC2547 concepts).
    
- Différence LDP vs RSVP (usage : LDP = distribution simple, RSVP = TE/reservation).
    

---

### ### Images à capturer (précis — screenshot these slides in the `Cisco Intro_to_mpls fr.pdf`)

(Use the slide numbers approximately shown in the PDF; they line up with the deck I cited.)

- **Label header (Label/EXP/S/TTL)** — capture slide ~10–11.
    
- **MPLS forwarding steps (push/swap/pop)** — slides ~14–16.
    
- **FEC → LSP mapping / label tables example** — slides ~20–25.
    
- **LDP neighbor & exchange concept** — slide ~25–27.
    
- **RSVP-TE PATH/RESV concept (TE overview)** — slide ~28.
    
- **Label stacking (internal/external labels, S bit)** — slides ~30–31.
    
- **VPN concepts intro (VPN L2 / L3) and VRF idea** — slides ~34–41 (stop here). These slides explain how MP-BGP and labels are used to separate VPN routing.
    

---

### ### Short practice drill (use these to self-test)

1. Draw the MPLS label stack for a packet entering PE for a VPNv4 route and explain what each label does.
    
2. Explain how LDP discovers neighbors and distributes labels (keywords: discovery, session, FEC).
    
3. In one sentence, explain difference between LDP and RSVP.  
    (Ask me for answers only after you try — I’ll guide you step by step.)
    

---

If you want, I’ll now:

- produce a **compact Markdown note** (Obsidian ready) containing the above text plus `![[...]]` placeholders named like you prefer (so you paste screenshots into `MPLS_LabelHeader.png`, etc.), **or**
    
- we can walk through the **first diagram** (label header) interactively — you try to screenshot it and paste it here (or tell me you captured it) and I’ll point out exactly what to annotate.
    

Which do you prefer next?