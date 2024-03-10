---
id: Network
created_date: 29/04/2023
updated_date: 29/04/2023
type: note
---

#  Network
- **🏷️Tags** :  #04-2023 #Network #basics #Proxies

## 📝 Notes

# Modèles de Réseau

Deux modèles de réseau décrivent la communication et le transfert de données d'un hôte à un autre, appelés modèle ISO/OSI et modèle TCP/IP. Il s'agit d'une représentation simplifiée des couches appelées transfert de bits en contenu lisible pour nous.

![[net_models4.png]]

## Le Modèle OSI

Le modèle OSI, souvent appelé modèle de couche ISO/OSI, est un modèle de référence pouvant être utilisé pour décrire et définir la communication entre les systèmes. Le modèle de référence comprend sept couches individuelles, chacune ayant des tâches clairement séparées.

Le terme OSI signifie Open Systems Interconnection model, publié par l'Union internationale des télécommunications (UIT) et l'Organisation internationale de normalisation (ISO). Par conséquent, le modèle OSI est souvent appelé le modèle de couche ISO/OSI.

>[!info]
il existe pleins de petites phrases pour se rappeler des différentes couches du modèle OSI, personnellement j'utilise la phrase suivante
> 	"**P**lease **D**o **N**ot **T**hrow the **S**ausage **p**izza **A**way" 

L'objectif de la norme ISO/OSI était de créer un modèle de référence qui permettrait la communication entre différents systèmes techniques via différents dispositifs et technologies tout en assurant la compatibilité. Le modèle OSI utilise sept couches différentes, hiérarchiquement basées les unes sur les autres pour atteindre cet objectif. Ces couches représentent les phases de l'établissement de chaque connexion à travers laquelle les paquets envoyés passent. Ainsi, la norme a été créée pour visualiser comment une connexion est structurée et établie.

| Couche | Fonction |
|--------|----------|
| 7. **Application** | Cette couche contrôle entre autres l'entrée et la sortie de données et fournit les fonctions d'application. |
| 6. **Présentation** | La tâche de la couche de présentation est de transférer la présentation des données dépendant du système en une forme indépendante de l'application. |
| 5. **Session** | La couche de session contrôle la connexion logique entre deux systèmes et évite, par exemple, les pannes de connexion ou autres problèmes. |
| 4. **Transport** | La couche 4 est utilisée pour le contrôle bout-à-bout des données transférées. La couche de transport peut détecter et éviter les situations de congestion et segmenter les flux de données. |
| 3. **Réseau** | Au niveau du réseau, les connexions sont établies dans les réseaux à commutation de circuit, et les paquets de données sont acheminés dans les réseaux à commutation de paquets. Les données sont transmises sur l'ensemble du réseau, de l'émetteur au destinataire. |
| 2. **Liaison de données** | La tâche centrale de la couche 2 est de permettre des transmissions fiables et sans erreur sur le support respectif. Pour ce faire, les flux de bits de la couche 1 sont divisés en blocs ou en trames. |
| 1. **Physique** | Les techniques de transmission utilisées sont, par exemple, des signaux électriques, optiques ou des ondes électromagnétiques. La transmission se fait par la couche 1 sur des lignes de transmission câblées ou sans fil. |


>[!info]
>Les couches 2 à 4 sont orientées transport, et les couches 5 à 7 sont orientées application. Dans chaque couche, des tâches précisément définies sont effectuées, et les interfaces avec les couches voisines sont précisément décrites. Chaque couche offre des services à utiliser pour la couche directement supérieure. Pour rendre ces services disponibles, la couche utilise les services de la couche inférieure et effectue les tâches de sa couche.
>
>Si deux systèmes communiquent, toutes les sept couches du modèle OSI sont traversées au moins deux fois, car l'émetteur et le récepteur doivent tenir compte du modèle de couche. Par conséquent, un grand nombre de tâches différentes doivent être effectuées dans les couches individuelles pour assurer la sécurité, la fiabilité et les performances de la communication.
>
>Lorsqu'une application envoie un paquet à l'autre système, le système travaille sur les couches mentionnées ci-dessus de la couche 7 à la couche 1, et le système récepteur

## Le Modèle TCP/IP

TCP/IP (Transmission Control Protocol/Internet Protocol) est un terme générique pour de nombreux protocoles de réseau. Les protocoles sont responsables de la commutation et du transport des paquets de données sur Internet. Internet est entièrement basé sur la famille de protocoles TCP/IP. Cependant, TCP/IP ne fait pas uniquement référence à ces deux protocoles, mais est généralement utilisé comme terme générique pour une famille de protocoles entière.

>[!info]
>Par exemple, ICMP (Internet Control Message Protocol) ou UDP (User Datagram Protocol) appartient à la famille de protocoles. La famille de protocoles fournit les fonctions nécessaires pour transporter et commuter des paquets de données dans un réseau privé ou public.
>
>IP se situe dans la couche réseau (couche 3) et TCP se situe dans la couche transport (couche 4) du modèle OSI en couches.

<u>Les couches sont les suivantes :</u>


|Couche | Fonction|
|--- | ---|
|**Application** | La couche application permet aux applications d'accéder aux services des autres couches et définit les protocoles que les applications utilisent pour échanger des données.|
|**Transport** | La couche transport est responsable de fournir des services de session TCP et de datagramme UDP pour la couche application.|
|**Internet** | La couche Internet est responsable des fonctions d'adressage, d'emballage et de routage des hôtes.|
|**Liaison** | La couche de liaison est responsable de la mise en place des paquets TCP/IP sur le support de réseau et de la réception des paquets correspondants du support de réseau. TCP/IP est conçu pour fonctionner indépendamment de la méthode d'accès au réseau, du format de trame et du support.|

Avec TCP/IP, chaque application peut transférer et échanger des données sur n'importe quel réseau, et il n'importe pas où se trouve le destinataire. IP assure que le paquet de données atteint sa destination, et TCP contrôle le transfert de données et assure la connexion entre le flux de données et l'application. La principale différence entre TCP/IP et OSI est le nombre de couches, dont certaines ont été combinées.

<u>Les tâches les plus importantes de TCP/IP sont :</u>

Tâche | Protocole | Description
--- | --- | ---
**Adressage logique** | IP | En raison de nombreux hôtes dans différents réseaux, il est nécessaire de structurer la topologie du réseau et l'adressage logique. Dans TCP/IP, IP prend en charge l'adressage logique des réseaux et des nœuds. Les paquets de données n'atteignent que le réseau où ils sont censés être. Les méthodes pour ce faire sont les classes de réseau, le sous-réseau et CIDR.
**Routage** | IP | Pour chaque paquet de données, le prochain nœud est déterminé dans chaque nœud sur le chemin de l'émetteur au récepteur. Ainsi, un paquet de données est acheminé vers son destinataire, même si sa position est inconnue de l'émetteur.
**Gestion des erreurs et de la circulation** | TCP | L'émetteur et le récepteur sont en contact fréquent via une connexion virtuelle. Par conséquent, des messages de contrôle sont envoyés en continu pour vérifier si la connexion est toujours établie.
**Prise en charge de l'application** | TCP | Les ports TCP et UDP forment une abstraction logicielle pour distinguer les applications spécifiques et leurs liens de communication.
**Résolution de noms** | DNS | DNS fournit la résolution de noms par le biais de noms de domaines complets (FQDN) en adresses IP, nous permettant d'atteindre l'hôte souhaité avec le nom spécifié sur Internet.

## ISO/OSI vs. TCP/IP

TCP/IP est un protocole de communication qui permet aux hôtes de se connecter à Internet. Il fait référence au protocole de contrôle de transmission utilisé dans et par les applications sur Internet. Contrairement à OSI, il permet un allègement des règles à suivre, à condition que des directives générales soient suivies.

>[!info]
>OSI, en revanche, est une passerelle de communication entre le réseau et les utilisateurs finaux. Le modèle OSI est généralement appelé modèle de référence car il est plus ancien. Il est également connu pour son protocole strict et ses limitations.

## Transfert de paquets

Dans un système en couches, les dispositifs d'une couche échangent des données dans un format différent appelé unité de données de protocole (PDU). Par exemple, lorsque nous voulons naviguer sur un site Web sur l'ordinateur, le logiciel du serveur distant passe d'abord les données demandées à la couche d'application. Elles sont traitées couche par couche, chaque couche effectuant ses fonctions assignées. Les données sont ensuite transférées à travers la couche physique du réseau jusqu'à ce que le serveur de destination ou un autre dispositif les reçoive. Les données sont acheminées à travers les couches à nouveau, chaque couche effectuant ses opérations assignées jusqu'à ce que le logiciel de réception utilise finalement les données.

![[net_models_pdu2.png]]

Pendant la transmission, chaque couche ajoute un en-tête à l'unité de données de protocole (PDU) de la couche supérieure, qui contrôle et identifie le paquet. Ce processus est appelé encapsulation. L'en-tête et les données forment ensemble la PDU pour la couche suivante. Le processus se poursuit jusqu'à la couche physique ou la couche réseau, où les données sont transmises au récepteur. Le récepteur inverse le processus et décompose les données couche par couche avec les informations d'en-tête. Ensuite, l'application utilise enfin les données. Ce processus continue jusqu'à ce que toutes les données aient été envoyées et reçues.

![[packet_transfer.png]]

Comme testeurs de pénétration, les deux modèles de référence sont utiles pour nous. Avec TCP/IP, nous pouvons rapidement comprendre comment toute la connexion est établie, et avec ISO, nous pouvons la décomposer pièce par pièce et l'analyser en détail. Cela se produit souvent lorsque nous pouvons écouter et intercepter un trafic réseau spécifique. Nous devons alors analyser ce trafic en conséquence, en allant plus en détail dans le module d'analyse de trafic réseau. Par conséquent, nous devrions nous familiariser avec les deux modèles de référence, les comprendre et les intérioriser de la meilleure façon possible.