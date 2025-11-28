**Partie théorique:** 
pfSense est un pare-feu open-source basé sur FreeBSD conçu pour fournir des fonctionnalités avancées de sécurité réseau. Il intègre un système de routage performant, la gestion des VLAN, le NAT, le VPN et un puissant filtrage des paquets via pf. pfSense offre une interface web intuitive permettant d’administrer facilement le trafic et les règles de sécurité. Grâce à ses nombreux packages, il peut être étendu pour inclure IDS/IPS, proxy, monitoring et services réseau. Sa stabilité et sa flexibilité en font une solution idéale pour les environnements professionnels et pédagogiques.


**Capture sur l’état de machine** 
![[Pasted image 20251128160936.png]]



**Ajout des règles de filtrage**

![[Pasted image 20251120124122.png]]


![[Pasted image 20251120124131.png]]




**Test depuis ma machine** 

![[Pasted image 20251120124408.png]]



**Accepter tout le trafic du LAN11(LAN) vers WAN**

![[Pasted image 20251120125825.png]]






**Test avec le tool ping du pfsense** 

![[Pasted image 20251120125714.png]]




**Accepter le trafic WEB du LAN vers un serveur WEB installé dans la**
**DMZ(LAN12)**


![[Pasted image 20251120130214.png]]






**Accepter le trafic DNS et WEB de DMZ vers WAN**


![[Pasted image 20251120130351.png]]
![[Pasted image 20251120130505.png]]





**Accepter le trafic WEB du WAN vers un serveur WEB installé dans la**
**DMZ(LAN12)**

![[Pasted image 20251120130653.png]]


**Règles pour refuser le reste de traffic** 


Dans le lan :

![[Pasted image 20251128161423.png]]


Dans la zone DMZ:

![[Pasted image 20251128161338.png]]