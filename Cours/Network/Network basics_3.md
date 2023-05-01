---
id: Network
created_date: 29/04/2023
updated_date: 29/04/2023
type: note
---

#  Network
- **🏷️Tags** :  #04-2023 #Network #basics #topologie

## 📝 Notes

## Topologies de réseau

Une topologie de réseau est un arrangement typique et une connexion physique ou logique des dispositifs dans un réseau. Les ordinateurs sont des hôtes, tels que les clients et les serveurs, qui utilisent activement le réseau. Ils comprennent également des composants réseau tels que les commutateurs, les ponts et les routeurs, que nous discuterons en détail dans les sections suivantes, qui ont une fonction de distribution et assurent que tous les hôtes du réseau peuvent établir une connexion logique les uns avec les autres. La topologie du réseau détermine les composants à utiliser et les méthodes d'accès au support de transmission.

>[!info]
>La disposition du support de transmission utilisée pour connecter les dispositifs est la topologie physique du réseau. Pour les supports conducteurs ou en fibre de verre, il s'agit du plan de câblage, des positions des nœuds et des connexions entre les nœuds et le câblage. En revanche, la topologie logique est la façon dont les signaux agissent sur les supports de réseau ou comment les données seront transmises à travers le réseau d'un dispositif à la connexion physique des dispositifs.

### Connexions 
| Wired connections    | Wireless connections |
|----------------------|----------------------|
| Coaxial cabling       | Wi-Fi                |
| Glass fiber cabling  | Cellular              |
| Twisted-pair cabling  | Satellite             |
| and others           | and others            |


### Nœuds - Contrôleur d'interface réseau (NIC) 

| Équipements de réseau  | Description |
| --- | --- |
| **Répéteurs** | Amplifient le signal d'un réseau |
| **Concentrateurs (Hubs)** | Permettent de connecter plusieurs appareils en un seul point |
| **Ponts (Bridges)** | Permettent de connecter des réseaux différents |
| **Commutateurs (Switches)** | Permettent de connecter plusieurs appareils en créant des connexions directes |
| **Routeur/Modem** | Permettent de connecter un réseau local à Internet |
| **Passerelles (Gateways)** | Permettent de connecter des réseaux différents en effectuant des conversions de protocoles |
| **Pare-feu (Firewalls)** | Protègent le réseau en bloquant le trafic non autorisé |


### Classifications

Nous pouvons imaginer une topologie comme une forme ou une structure virtuelle d'un réseau. Cette forme ne correspond pas nécessairement à l'arrangement physique réel des dispositifs dans le réseau. Par conséquent, ces topologies peuvent être soit physiques soit logiques.

| Topologie réseau   | Description                                                                                                               |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------|
| **Point à Point**         | La topologie point à point relie deux nœuds directement ensemble à travers un lien dédié.                                  |
| **Bus**                   | Dans la topologie bus, tous les nœuds sont connectés à une ligne de communication principale.                                |
| **Étoile**                | Dans une topologie en étoile, chaque nœud est connecté à un nœud central.                                                   |
| **Anneau**                | Les nœuds dans une topologie en anneau sont connectés dans une boucle en utilisant un lien unidirectionnel.                  |
| **Mesh**                  | Dans une topologie mesh, chaque nœud est connecté à tous les autres nœuds du réseau.                                          |
| **Arbre**                 | Dans une topologie en arbre, les nœuds sont organisés dans une hiérarchie avec un nœud central qui contrôle les nœuds plus bas.|
| **Hybride**               | Les topologies hybrides combinent deux ou plusieurs topologies différentes.                                                  |
| **Chaîne en série (ou Daisy Chain)** | Dans une topologie en chaîne, les nœuds sont connectés les uns aux autres dans une séquence linéaire.           | 



## Topologie point à point

La topologie de réseau la plus simple avec une connexion dédiée entre deux hôtes est la topologie point à point. Dans cette topologie, il n'existe qu'un lien physique direct et simple entre deux hôtes. Ces deux dispositifs peuvent utiliser ces connexions pour une communication mutuelle.

Les topologies point à point sont le modèle de base de la téléphonie traditionnelle et ne doivent pas être confondues avec l'architecture P2P

![[topo_p2p.png]]

## Topologie en Bus

Dans la topologie en bus, tous les hôtes sont connectés via un support de transmission commun. Chaque hôte a accès au support de transmission et aux signaux qui y sont transmis. Il n'y a pas de composant central du réseau qui contrôle les processus. Le support de transmission peut être un câble coaxial.

![[topo_bus.png]]

## Topologie en Étoile

Dans la topologie en étoile, chaque hôte est connecté au composant central du réseau via un lien séparé. Le composant central est généralement un routeur, un concentrateur ou un commutateur. Les paquets de données sont reçus et transmis vers leur destination par le composant central. Le trafic de données sur le composant central peut être très élevé puisque toutes les données et les connexions passent par lui.

![[topo_star.png]]

## Topologie en Anneau

Dans la topologie en anneau, chaque hôte est connecté à l'anneau avec deux câbles : un pour les signaux entrants et un autre pour les signaux sortants. Le contrôle et l'accès au support de transmission sont régulés par un protocole auquel toutes les stations adhèrent.

![[topo_ring.png]]

## Topologie en Maillage

Dans les réseaux en maillage, les nœuds décident des connexions au niveau physique et du routage au niveau logique. Il n'y a pas de topologie fixe. Il y a deux structures de base: la structure entièrement maillée et la structure partiellement maillée.

![[topo_mesh.png]]

## Topologie en Arbre

La topologie en arbre est une extension de la topologie en étoile. Cette topologie est utile lorsque plusieurs topologies sont combinées. Elle est souvent utilisée dans les grands bâtiments d'entreprise.

![[topo_tree.png]]

## Topologie Hybride

Les réseaux hybrides combinent deux ou plusieurs topologies pour obtenir un réseau sans topologie standard.

![[topo_hybrid.png]]

## Topologie en Chaîne

Dans la topologie en chaîne, plusieurs hôtes sont connectés en plaçant un câble d'un nœud à l'autre. Cette configuration est souvent utilisée dans la technologie de l'automatisation.


![[topo_daisy-chain.png]]


## Questions/Thoughts


## 🔗 Links
- 