---
id: Network
created_date: 29/04/2023
updated_date: 29/04/2023
type: note
---

#  Network
- **🏷️Tags** :  #04-2023 #Network #basics #Proxies

## 📝 Notes

## Adressage

La couche réseau (Couche 3) de l'OSI contrôle l'échange de paquets de données, car ces derniers ne peuvent pas être directement routés vers le destinataire et doivent donc être dotés de nœuds de routage.

Les paquets de données sont ensuite transférés de nœud en nœud jusqu'à ce qu'ils atteignent leur destination. Pour mettre en œuvre cela, la couche réseau identifie les nœuds individuels du réseau, établit et libère les canaux de connexion, et s'occupe du routage et de la régulation du flux de données. Lors de l'envoi des paquets, les adresses sont évaluées et les données sont acheminées à travers le réseau de nœud en nœud.

Il n'y a généralement pas de traitement des données dans les couches supérieures à la L3 dans les nœuds. En fonction des adresses, le routage et la construction des tables de routage sont effectués.

>[!info]
>En bref, il est responsable des fonctions suivantes :
>	-   Adressage logique
>	-   Routage

Les protocoles sont définis dans chaque couche de l'OSI, et ces protocoles représentent une collection de règles pour la communication dans la couche respective. Ils sont transparents aux protocoles des couches supérieures ou inférieures. Certains protocoles remplissent des tâches de plusieurs couches et s'étendent sur deux couches ou plus. Les protocoles les plus utilisés dans cette couche sont :

| Protocoles | Description |
|-----------|-------------|
| **IPv4 / IPv6** | Protocoles de communication pour l'envoi de paquets de données à travers le réseau. |
| **IPsec** | Protocole de sécurité pour l'authentification et la confidentialité des paquets IP. |
| **ICMP** | Protocole de contrôle et de gestion des erreurs pour les paquets IP. |
| **IGMP** | Protocole de gestion de groupe Internet pour la diffusion de données multimédia en continu. |
| **RIP** | Protocole de routage à vecteur de distance pour les réseaux de taille moyenne. |
| **OSPF** | Protocole de routage à état de lien pour les réseaux de grande taille. |


La couche réseau assure le routage des paquets de la source vers la destination à l'intérieur ou à l'extérieur d'un sous-réseau. Ces deux sous-réseaux peuvent avoir des schémas d'adressage différents ou des types d'adressage incompatibles.
Dans les deux cas, la transmission des données passe par l'ensemble du réseau de communication et comprend le routage entre les nœuds du réseau. Étant donné que la communication directe entre l'expéditeur et le destinataire n'est pas toujours possible en raison des sous-réseaux différents, les paquets doivent être transférés par des nœuds (routeurs) qui se trouvent sur le chemin.

Les paquets transférés n'atteignent pas les couches supérieures mais se voient attribuer une nouvelle destination intermédiaire et sont envoyés au nœud suivant.

## Les adresses IP

Chaque hôte du réseau peut être identifié par une adresse MAC (Media Access Control) qui permet l'échange de données dans ce réseau. Si l'hôte distant est situé dans un autre réseau, la connaissance de l'adresse MAC ne suffit pas pour établir une connexion. L'adressage sur Internet se fait via l'adresse IPv4 et/ou IPv6, qui est composée de l'adresse de réseau et de l'adresse d'hôte.

Peu importe qu'il s'agisse d'un réseau plus petit, tel qu'un réseau d'ordinateurs domestiques, ou de l'ensemble d'Internet. L'adresse IP assure la livraison des données au bon destinataire. On peut imaginer la représentation des adresses MAC et IPv4/IPv6 comme suit :

>[!info]
> - IPv4/IPv6 - décrit l'adresse postale unique et le quartier du bâtiment du destinataire.
> - MAC - décrit l'étage exact et l'appartement du destinataire. Il est possible pour une seule adresse IP d'adresser plusieurs destinataires (diffusion) ou pour un appareil de répondre à plusieurs adresses IP. Cependant, il faut s'assurer que chaque adresse IP est assignée une seule fois dans le réseau.

## Structure d'IPv4

La méthode la plus courante d'attribution des adresses IP est IPv4, qui est composé d'un nombre binaire de 32 bits combiné en 4 octets de 8 bits chacun (octets) allant de 0 à 255. Ces octets sont convertis en nombres décimaux plus facilement lisibles, séparés par des points et représentés sous forme de notation décimale pointée.

Ainsi, une adresse IPv4 peut ressembler à ceci :

>Notation Présentation Binaire 0111 1111.0000 0000.0000 0000.0000 0001 Décimal 127.0.0.1

Chaque interface réseau (cartes réseau, imprimantes réseau ou routeurs) se voit attribuer une adresse IP unique.

Le format IPv4 permet 4 294 967 296 adresses uniques. L'adresse IP est divisée en une partie hôte et une partie réseau. Le routeur assigne la partie hôte de l'adresse IP à domicile ou par un administrateur. La partie réseau respective est attribuée par l'administrateur du réseau. Sur Internet, il s'agit de l'IANA, qui alloue et gère les adresses IP uniques.

Dans le passé, une classification supplémentaire était effectuée ici. Les blocs de réseau IP étaient divisés en classes A - E. Les différentes classes différaient dans les longueurs respectives des parts d'hôtes et de réseaux.

|Class | Network Address | First Address | Last Address | Subnetmask | CIDR | Subnets | IPs|
|----- | --------------- | ------------- | ------------ | ---------- | ---- | ------- | ---|
|A | 1.0.0.0 | 1.0.0.1 | 127.255.255.255 | 255.0.0.0 | /8 | 127 | 16,777,214 + 2 |
|B | 128.0.0.0 | 128.0.0.1 | 191.255.255.255 | 255.255.0.0 | /16 | 16,384 | 65,534 + 2|
|C | 192.0.0.0 | 192.0.0.1 | 223.255.255.255 | 255.255.255.0 | /24 | 2,097,152  254 + 2|
|D | 224.0.0.0 | 224.0.0.1 | 239.255.255.255 | Multicast | Multicast | Multicast | Multicast|
|E | 240.0.0.0 | 240.0.0.1 | 255.255.255.255 | reserved | reserved | reserved | reserved|

## Subnet Mask

La sub****division supplémentaire de ces classes en petits réseaux est effectuée à l'aide du sous-réseau (subnetting). Cette séparation est réalisée à l'aide de masques de réseau (netmasks), qui sont aussi longs qu'une adresse IPv4. Tout comme les classes, ils décrivent quelles positions de bits dans l'adresse IP agissent comme partie réseau ou partie hôte.

| Classe | Adresse de réseau | Première adresse | Dernière adresse | **Masque de sous-réseau** | CIDR | Sous-réseaux | Adresses IP |
|--------|------------------|------------------|-----------------|-----------------------|------|-------------|-------------|
| A      | 1.0.0.0          | 1.0.0.1          | 127.255.255.255 | **255.0.0.0**             | /8   | 127         | 16 777 214 + 2 |
| B      | 128.0.0.0        | 128.0.0.1        | 191.255.255.255 | **255.255.0.0**           | /16  | 16 384      | 65 534 + 2     |
| C      | 192.0.0.0        | 192.0.0.1        | 223.255.255.255 | **255.255.255.0**         | /24  | 2 097 152   | 254 + 2        |
| D      | 224.0.0.0        | 224.0.0.1        | 239.255.255.255 | **Multicast**             | Multicast | Multicast | Multicast |
| E      | 240.0.0.0        | 240.0.0.1        | 255.255.255.255 | **Réservé**               | Réservé | Réservé     | Réservé     |

## Adresses de réseau et de passerelle

Les deux adresses IP supplémentaires ajoutées dans la colonne des adresses IP sont réservées à l'adresse réseau et à l'adresse de diffusion. Une autre adresse importante est celle de la passerelle par défaut, qui est le nom de l'adresse IPv4 du routeur qui relie les réseaux et les systèmes avec différents protocoles et gère les adresses et les méthodes de transmission. Il est courant que la passerelle par défaut soit assignée à la première ou la dernière adresse IPv4 assignable dans un sous-réseau. Ce n'est pas une exigence technique, mais c'est devenu une norme de facto dans les environnements réseau de toutes tailles.

|Class | Network Address | **First Address** | Last Address | Subnetmask | CIDR | Subnets | **IPs**|
|----- | --------------- | ------------- | ------------ | ---------- | ---- | ------- | ---|
|A | 1.0.0.0 | **1.0.0.1** | 127.255.255.255 | 255.0.0.0 | /8 | 127 | 16,777,214 **+ 2** |
|B | 128.0.0.0 | **128.0.0.1** | 191.255.255.255 | 255.255.0.0 | /16 | 16,384 | 65,534 **+ 2**|
|C | 192.0.0.0 | **192.0.0.1** | 223.255.255.255 | 255.255.255.0 | /24 | 2,097,152  254 **+ 2**|
|D | 224.0.0.0 | **224.0.0.1** | 239.255.255.255 | Multicast | Multicast | Multicast | Multicast|
|E | 240.0.0.0 | **240.0.0.1** | 255.255.255.255 | reserved | reserved | reserved | reserved|


## Broadcast

### Adresses de réseau et de diffusion

Les deux adresses IP supplémentaires ajoutées dans la colonne des adresses IP sont réservées à l'adresse de réseau et à l'adresse de diffusion. La diffusion dans un réseau est un message qui est transmis à tous les participants du réseau et ne nécessite aucune réponse. De cette façon, un hôte envoie un paquet de données à tous les autres participants du réseau simultanément et, ce faisant, communique son adresse IP, que les destinataires peuvent utiliser pour le contacter. C'est la dernière adresse IPv4 utilisée pour la diffusion.

### Adresse de passerelle

Une autre adresse importante est celle de la passerelle par défaut, qui est le nom donné à l'adresse IPv4 du routeur qui couple des réseaux et des systèmes avec différents protocoles et gère les adresses et les méthodes de transmission. Il est courant que la passerelle par défaut soit affectée à la première ou à la dernière adresse IPv4 attribuable dans un sous-réseau. Ceci n'est pas une exigence technique, mais est devenu une norme de facto dans les environnements de réseau de toutes tailles.

|Class | Network Address | First Address | **Last Address** | Subnetmask | CIDR | Subnets | IPs|
|----- | --------------- | ------------- | ------------ | ---------- | ---- | ------- | ---|
|A | 1.0.0.0 | 1.0.0.1 | **127.255.255.255** | 255.0.0.0 | /8 | 127 | 16,777,214 + 2 |
|B | 128.0.0.0 | 128.0.0.1 | **191.255.255.255** | 255.255.0.0 | /16 | 16,384 | 65,534 + 2|
|C | 192.0.0.0 | 192.0.0.1 | **223.255.255.255** | 255.255.255.0 | /24 | 2,097,152  254 + 2|
|D | 224.0.0.0 | 224.0.0.1 | **239.255.255.255** | Multicast | Multicast | Multicast | Multicast|
|E | 240.0.0.0 | 240.0.0.1 | **255.255.255.255** | reserved | reserved | reserved | reserved|

## Système binaire

Le système binaire est un système de numération qui n'utilise que deux états différents qui sont représentés par deux chiffres (0 et 1) opposés au système décimal (0 à 9).

Une adresse IPv4 est divisée en 4 octets, comme nous l'avons déjà vu. Chaque octet se compose de 8 bits. Chaque position d'un bit dans un octet a une valeur décimale spécifique. Prenons l'adresse IPv4 suivante comme exemple:

> IPv4 Address: 192.168.10.39
> Voici un exemple de la façon dont le premier octet ressemble:

```
> 1er octet - Valeur: 192
> Valeurs:         128  64  32  16  8  4  2  1
> Binaire:           1   1   0   0  0  0  0  0
```


Si nous calculons la somme de toutes ces valeurs pour chaque octet où le bit est défini à 1, nous obtenons la somme :

| Octet | Valeurs                            | Somme |
|-------|-----------------------------------|-------|
| 1er   | 128 + 64 + 0 + 0 + 0 + 0 + 0 + 0   | 192   |
| 2ème  | 128 + 0 + 32 + 0 + 8 + 0 + 0 + 0   | 168   |
| 3ème  | 0 + 0 + 0 + 0 + 8 + 0 + 2 + 0       | 10    |
| 4ème  | 0 + 0 + 32 + 0 + 0 + 4 + 2 + 1      | 39    |

La représentation complète de binaire à décimal ressemblerait à ceci:

| Octet | Valeurs | 
|-------|--------|
| 1er   | 128 + 64 + 0 + 0 + 0 + 0 + 0 + 0   = 192 |
| 2ème  | 128 + 0 + 32 + 0 + 8 + 0 + 0 + 0   = 168 |
| 3ème  | 0 + 0 + 0 + 0 + 8 + 0 + 2 + 0       = 10  |
| 4ème  | 0 + 0 + 32 + 0 + 0 + 4 + 2 + 1      = 39  |


Cette addition a lieu pour chaque octet, ce qui donne une représentation décimale de l'adresse IPv4. Le masque de sous-réseau est calculé de la même manière.

## CIDR

>[!info]
>Classless Inter-Domain Routing ( CIDR) est une méthode de représentation et remplace l'affectation fixe entre l'adresse IPv4 et les classes de réseau (A, B, C, D, E). La division est basée sur le masque de sous-réseau ou le soi-disant CIDR suffix, qui permet la division au niveau du bit de l'espace d'adressage IPv4 et donc en subnets de n'importe quelle taille. Le CIDR suffix indique combien de bits depuis le début de l'adresse IPv4 appartiennent au réseau. C'est une notation qui représente le subnet mask en spécifiant le nombre de 1-bits dans le masque de sous-réseau.

Tenons-nous en à l'adresse IPv4 et au masque de sous-réseau suivants à titre d'exemple :

-   Adresse IPv4 :192.168.10.39
 
-   Masque de sous-réseau :255.255.255.0

Maintenant, la représentation complète de l'adresse IPv4 et du masque de sous-réseau ressemblerait à ceci :

-   CIDR :192.168.10.39/24

Le suffixe CIDR est donc la somme de tous les uns dans le masque de sous-réseau.

  Masque de sous-réseau

```shell-session
Octet:             1st         2nd         3rd         4th
Binary:         1111 1111 . 1111 1111 . 1111 1111 . 0000 0000 (/24)
Decimal:           255    .    255    .    255    .     0
```