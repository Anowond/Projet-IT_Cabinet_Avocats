
# Cabinets d'avocats Dupont & Associés

Projet personnel de conception et paramétrage d'un réseau de type SOHO

Le fichier Packet Tracer est mis à disposition dans le repository



## Contexte

Le cabinet d'avocats Dupont & Associés à besoin d'un administrateur pour concevoir, configurer et gérer le réseau informatique de son agence; celle-ci se compose :

- De 3 avocats
- D'un parajuriste
- D'un chargé d'acceuil

Chaque membre du personnel de l'agence se doit d'avoir son propre téléphone fixe à son bureau pour travailler, ainsi qu'un accés à un photocopieur qui lui sera commun.

Il est également éxigé qu'un moyen de connexion sans-fil soit mis à disposition des clients de l'agence, afin qu'ils puissent accéder à internet et à leur ressrouces distantes depuis leur appareils portatifs (sans toutefois avoir accés aux ressources de l'agence).



## Topologie

<img width="1191" height="690" alt="image" src="https://github.com/user-attachments/assets/8249a354-ac20-4ffc-afe7-194c94b5694a" />

## Plan d'adressage

- @ WAN : 203.0.113.45

- VLAN 10 : AVOCATS         192.168.10.0 /24
- VLAN 20 : PARAJURISTES    192.168.20.0 /24
- VLAN 30 : ACCEUIL         192.168.30.0 /24
- VLAN 40 : COPIEURS        192.168.40.0 /24
- VLAN 50 : TELEPHONES      192.168.50.0 /24
- VLAN 60 : WIFI            192.168.60.0 /24
- VLAN 99 : MANAGMENT       192.168.99.0 /24
- VLAN 999 : BLACKHOLE

- Serveur DHCP : DST-SW1
    - Attriubtion dynamique des addresses pour les VLANs 10,20,30,50 et 60


## Sécurité

- Blackhole VLAN 999 pour les interfaces inutilisées
- VLAN par défaut 999 sur DST-SW1 et ACC-SW1
- Seuls les VLANs 10,20,30,40,50,60 et 99 sont autorisés sur les liens trunks
- ACL étendue RESTREINDRE_GUESTS sur DST-SW1 :
    - Interdit le traffic provenant du vlan 60 aux autres VLANs
- ACL standard 10 sur EDGE-RTR, DST-SW1 et ACC-SW1 :
    - Autorise l'accéss aux lignes vty 0 15 seulement au VLAN 99 (admins)
- Configuration du service DHCP Snooping sur ACC-SW1
- SSH configuré sur chaque équipement



## Mots de passe

- Mode privilégié : Cisco123!
- SSH : Ssh123!
- VTP : Vtp123!

- WIFI :
    - SSID : DUPONT&CO_WIFI
    - MDP : P4ssw0rd 

