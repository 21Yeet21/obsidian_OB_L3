# Best-practice-for-network-segmentation

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#best-practice-for-network-segmentation)

## What is this?

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#what-is-this)

This project was created to publish the best practices for segmentation of the corporate network of any company. In general, the schemes in this project are suitable for any company.

## Where can I find diagrams?

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#where-can-i-find-diagrams)

Graphic diagrams are available in the [Release page](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/releases)  
The schema sources are located in the [repository](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/tree/main)

## Schematic symbols

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#schematic-symbols)

Elements used in network diagrams:  
[![Schematic symbols](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/raw/main/Schematic%20symbols/Schematic%20symbols.jpg)](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/blob/main/Schematic%20symbols/Schematic%20symbols.jpg)  
Crossing the border of the rectangle means crossing the firewall.

## Level 1 of network segmentation: basic segmentation  

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#level-1-of-network-segmentation-basic-segmentation)

[![Level 1](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/releases/download/4.1.1/Network.segmentation.Level.1.jpg)](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/releases/download/4.1.1/Network.segmentation.Level.1.jpg)

### Advantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#advantages)

Basic segmentation to protect against basic targeted attacks that make it difficult for an attacker to advance on the network. Basic isolation of the productive environment from the corporate one.

### Disadvantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#disadvantages)

The default corporate network should be considered potentially compromised. Potentially compromised workstations of ordinary workers, as well as workstations of administrators, have basic and administrative access to the production network.

In this regard, the compromise of any workstation can theoretically lead to the exploitation of the following attack vector. An attacker compromises a workstation in the corporate network. Further, the attacker either elevates privileges in the corporate network or immediately attacks the production network with the rights that the attacker had previously obtained.

### Attack vector protection

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#attack-vector-protection)

Installation the maximum number of information protection tools, real time monitoring suspicious events and immediate response.  
OR!  
Segmentation according to level 2 requirements  

## Level 2 of network segmentation: adoption of basic security practices  

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#level-2-of-network-segmentation-adoption-of-basic-security-practices)

[![Level 2](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/releases/download/4.1.1/Network.segmentation.Level.2.jpg)](https://github.com/sergiomarotco/Best-practice-for-network-segmentation/releases/download/4.1.1/Network.segmentation.Level.2.jpg)

### Advantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#advantages-1)

More network segments in the corporate network.  
Full duplication of the main supporting infrastructure for production network such as:

1. mail relays;
2. time servers;
3. other services, if available.  
    

Safer software development. Recommended implementing DevSecOps at least Level 1 of the [DSOMM](https://dsomm.owasp.org/circular-heatmap), what requires the introduction of a separate storage of secrets for passwords, tokens, cryptographic keys, logins, etc., additional servers for SAST, DAST, fuzzing, SCA and another DevSecOps tools. In case of problems in the supporting infrastructure in the corporate segment, this will not affect the production environment. It is a little harder for an attacker to compromise a production environment.  
Or you can implement at least Level 2 of the [SLSA](https://slsa.dev/).

### Disadvantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#disadvantages-1)

As a result, this leads to the following problems:

1. increasing the cost of ownership and the cost of final services to customers;
2. high complexity of maintenance.

## Level 3 of network segmentation: high adoption of security practices  

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#level-3-of-network-segmentation-high-adoption-of-security-practices)

The company's management (CEO) understands the role of cybersecurity in the life of the company. Information security risk becomes one of the company's operational risks. Depending on the size of the company, the minimum size of an information security unit is 15-20 employees. [![Level 3](https://github.com/sergiomarotco/network-segmentation-cheet-sheet/releases/download/4.1.1/Network.segmentation.Level.3.jpg)](https://github.com/sergiomarotco/network-segmentation-cheet-sheet/releases/download/4.1.1/Network.segmentation.Level.3.jpg)

### Advantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#advantages-2)

Implementing security services such us:

1. security operation center (SIEM, IRP, SOAR, SGRC);
2. data leak prevention;
3. phishing protection;
4. sandbox;
5. intrusion prevention system;
6. vulnerability scanner;
7. endpoint and ATP protection;
8. web application firewall;
9. backup server.

### Disadvantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#disadvantages-2)

High costs of information security tools and information security specialists.

## Level 4 of network segmentation: advanced deployment of security practices at scale

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#level-4-of-network-segmentation-advanced-deployment-of-security-practices-at-scale)

Each production and corporate services has its own networks: Tier I, Tier II, Tier III.

The production environment is accessed from isolated computers. This type of segmentation is called an air gap, this is close to protecting state secrets. Each isolated computer does not have:

1. incoming accesses from anywhere except from remote corporate laptops via VPN;
2. outgoing access to the corporate network:
    - no access to the mail service - the threat of spear phishing is not possible;
    - there is no access to internal sites and services - it is impossible to download a trojan from a compromised corporate networks.

🔥Only one way to compromise an isolated computer is to compromise the production environment. As a result, a successful compromise of a computer, even by phishing, will prevent a hacker from gaining access to a production environment.

Implement other possible security services, such as:

1. privileged access management;
2. internal phishing training server;
3. compliance server (configuration assessment).

[![Level 4](https://raw.githubusercontent.com/sergiomarotco/Network-segmentation-cheat-sheet/main/Network%20segmentation%20Level%204.jpg)](https://raw.githubusercontent.com/sergiomarotco/Network-segmentation-cheat-sheet/main/Network%20segmentation%20Level%204.jpg)

### Advantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#advantages-3)

Implementing security services such us:

1. privileged access management;
2. internal phishing training server;
3. compliance server (configuration assessment);
4. strong protection of your production environment from spear phishing.

🔥Now the attacker will not be able to attack the production network, because now a potentially compromised workstation in the corporate network basically does not have network access to the production. Related problems:

1. separate workstations for access to the production network - yes, now you will have 2 computers on your desktop;
2. other LDAP catalog or Domain controller for production network;
3. firewall analyzer, network equipment analyzer;
4. netflow analyzer.

[![hippo](https://raw.githubusercontent.com/sergiomarotco/Network-segmentation-cheat-sheet/main/Other/Powtoon_GIF.gif)](https://raw.githubusercontent.com/sergiomarotco/Network-segmentation-cheat-sheet/main/Other/Powtoon_GIF.gif)

### Disadvantages

[](https://github.com/sergiomarotco/Network-segmentation-cheat-sheet#disadvantages-3)

Now you will have 2 computers on your desktop if you need access to production network. It hurts 😀