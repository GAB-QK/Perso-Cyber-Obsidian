---
id: Network
created_date: 29/04/2023
updated_date: 29/04/2023
type: note
---

#  Network
- **🏷️Tags** :  #04-2023 #Network #basics #Proxies

## 📝 Notes

### Adressage MAC

---

Chaque hôte d'un réseau possède sa propre adresse `48`-bit ( `6 octets`) `Media Access Control` ( MAC ), représentée au format hexadécimal. est le pour nos interfaces réseau. Il existe plusieurs normes différentes pour l'adresse MAC.

-   Ethernet (IEEE 802.3)
-   Bluetooth (IEEE 802.15)
-   WLAN (IEEE 802.11)

En effet, les adresses `MAC`  adresse la connexion physique (carte réseau, Bluetooth ou adaptateur WLAN) d'un hôte. Chaque carte réseau a son adresse MAC individuelle, qui est configurée une fois du côté matériel du fabricant mais qui peut toujours être modifiée, au moins temporairement.

Examinons un exemple d'une telle adresse MAC :

Adresse Mac:

-   `DE:AD:BE:EF:13:37`
-   `DE-AD-BE-EF-13-37`
-   `DEAD.BEEF.1337`

| Representation | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | 5th Octet | 6th Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | 1101 1110 | 1010 1101 | 1011 1110 | 1110 1111 | 0001 0011 | 0011 0111 |
| Hex | DE | AD | BE | EF | 13 | 37 |

---

>[!info]
>Lorsqu'un paquet IP est livré, il doit être adressé `layer 2`à l'adresse physique de l'hôte de destination ou au routeur/NAT, qui est responsable du routage. Chaque paquet a un `sender address`et un `destination address`.

L'adresse MAC se compose d'un total de `6 bytes`. La première moitié ( `3 bytes`/ `24 bit`) est ce qu'on appelle `Organization Unique Identifier`( `OUI`) défini par le `Institute of Electrical and Electronics Engineers`( `IEEE`) pour les fabricants respectifs.

| Representation | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | 5th Octet | 6th Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | **1101 1110** | **1010 1101** | **1011 1110** | 1110 1111 | 0001 0011 | 0011 0111 |
| Hex | **DE** | **AD** | **BE** | EF | 13 | 37 |

---

La dernière moitié de l'adresse MAC est appelée le `Individual Address Part`ou `Network Interface Controller`( `NIC`), que les fabricants attribuent. Le fabricant définit cette séquence de bits une seule fois et garantit ainsi que l'adresse complète est unique.

| Representation | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | 5th Octet | 6th Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | 1101 1110 | 1010 1101 | **1011 1110** | **1110 1111** | **0001 0011** | **0011 0111** |
| Hex | DE | AD | BE | **EF** | **13** | **37** |

Si un hôte avec l'adresse IP cible se trouve dans le même sous-réseau, la livraison est effectuée directement à l'adresse physique de l'ordinateur cible. Cependant, si cet hôte appartient à un sous-réseau différent, la trame Ethernet est adressée au `MAC address`routeur responsable ( `default gateway`). Si l'adresse de destination de la trame Ethernet correspond à la sienne `layer 2 address`, le routeur transmet la trame aux couches supérieures. `Address Resolution Protocol`( `ARP`) est utilisé dans IPv4 pour déterminer les adresses MAC associées aux adresses IP.


>[!info]
>Comme pour les adresses IPv4, il existe également certaines zones réservées pour l'adresse MAC. Celles-ci incluent, par exemple, la plage locale pour le MAC.

| **Local Range**     |
| ------------------- |
| 0`2`:00:00:00:00:00 |
| 0`6`:00:00:00:00:00 |
| 0`A`:00:00:00:00:00 |
| 0`E`:00:00:00:00:00 |

De plus, les deux derniers bits du premier octet peuvent jouer un autre rôle essentiel. Le dernier bit peut avoir deux états, 0 et 1, comme nous le savons déjà. Le dernier bit identifie l'adresse MAC comme `Unicast`( `0`) ou `Multicast`( `1`). Avec `unicast`, cela signifie que le paquet envoyé n'atteindra qu'un seul hôte spécifique.

#### MAC Unicast

| Representation | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | 5th Octet | 6th Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | 1101 111**0** | 1010 1101 | 1011 1110 | 1110 1111 | 0001 0011 | 0011 0111 |
| Hex | D**E** | AD | BE | EF | 13 | 37 |

---

Avec `multicast`, le paquet n'est envoyé qu'une seule fois à tous les hôtes du réseau local, qui décident alors d'accepter ou non le paquet en fonction de leur configuration. L' `multicast` adresse est une adresse unique, tout comme l' `broadcast` adresse, qui a des valeurs d'octet fixes. `Broadcast` dans un réseau représente un appel diffusé, où les paquets de données sont transmis simultanément d'un point à tous les membres d'un réseau. Il est principalement utilisé si l'adresse du destinataire du paquet n'est pas encore connue. Un exemple est les protocoles `ARP`( `for MAC addresses`) et DHCP ( `for IPv4 addresses`).

Les valeurs définies de chaque octet sont marquées `green`.

#### MAC Multicast

| Représentation | 1er Octet | 2ème Octet | 3ème Octet | 4ème Octet | 5ème Octet | 6ème Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | **0000 0001** | **0000 0000** | **0101 1110** | 1110 1111 | 0001 0011 | 0011 0111 |
| Hex | **01** | **00** | **5E** | EF | 13 | 37 |


#### MAC Broadcast

| Représentation | 1er Octet | 2ème Octet | 3ème Octet | 4ème Octet | 5ème Octet | 6ème Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | **1111 1111** | **1111 1111** | **1111 1111** | **1111 1111** | **1111 1111** | **1111 1111** |
| Hex | **FF** | **FF** | **FF** | **FF** | **FF** | **FF** |

---

L'avant-dernier bit du premier octet identifie s'il s'agit d'une adresse `global OUI`, définie par l'IEEE, ou d'une `locally administrated` adresse MAC.

#### Global OUI

| Representation | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | 5th Octet | 6th Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | 1101 11**0**0 | 1010 1101 | 1011 1110 | 1110 1111 | 0001 0011 | 0011 0111 |
| Hex | D**C** | AD | BE | EF | 13 | 37 |

#### Locally Administrated

| Representation | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet | 5th Octet | 6th Octet |
| --- | --- | --- | --- | --- | --- | --- |
| Binary | 1101 11**1**0 | 1010 1101 | 1011 1110 | 1110 1111 | 0001 0011 | 0011 0111 |
| Hex | D**E** | AD | BE | EF | 13 | 37 |

---

## Protocole de résolution d'adresse

Les adresses MAC peuvent être modifiées/manipulées ou usurpées, et en tant que telles, elles ne doivent pas être considérées comme un seul moyen de sécurité ou d'identification. Les administrateurs réseau doivent mettre en œuvre des mesures de sécurité supplémentaires, telles que la segmentation du réseau et des protocoles d'authentification forts, pour se protéger contre les attaques potentielles.

Il existe plusieurs vecteurs d'attaque potentiellement exploitables via l'utilisation d'adresses MAC :

-   `MAC spoofing`: cela implique de modifier l'adresse MAC d'un appareil pour qu'elle corresponde à celle d'un autre appareil, généralement pour obtenir un accès non autorisé à un réseau.
    
-   `MAC flooding`: cela implique l'envoi de nombreux paquets avec différentes adresses MAC à un commutateur réseau, l'amenant à atteindre sa capacité de table d'adresses MAC et l'empêchant effectivement de fonctionner correctement.
    
-   `MAC address filtering`: Certains réseaux peuvent être configurés uniquement pour autoriser l'accès à des appareils avec des adresses MAC spécifiques que nous pourrions potentiellement exploiter en tentant d'accéder au réseau à l'aide d'une adresse MAC usurpée.
    

---

## Protocole de résolution d'adresse

[Le protocole de résolution d'adresse](https://en.wikipedia.org/wiki/Address_Resolution_Protocol) ( `ARP` ) est un protocole réseau. Il s'agit d'une partie importante de la communication réseau utilisée pour résoudre une adresse IP de couche réseau (couche 3) en une adresse MAC de couche liaison (couche 2). Il mappe l'adresse IP d'un hôte à son adresse MAC correspondante pour faciliter la communication entre les périphériques sur un [réseau local](https://en.wikipedia.org/wiki/Local_area_network) ( `LAN` ). Lorsqu'un périphérique sur un réseau local souhaite communiquer avec un autre périphérique, il envoie un message de diffusion contenant l'adresse IP de destination et sa propre adresse MAC. L'appareil avec l'adresse IP correspondante répond avec sa propre adresse MAC, et les deux appareils peuvent alors communiquer directement en utilisant leurs adresses MAC. Ce processus est connu sous le nom de résolution ARP.

ARP est une partie importante du processus de communication réseau car il permet aux appareils d'envoyer et de recevoir des données à l'aide d'adresses MAC plutôt que d'adresses IP, ce qui peut être plus efficace. Deux types de messages de requête peuvent être utilisés :

#### Demande ARP

Lorsqu'un appareil souhaite communiquer avec un autre appareil sur un réseau local, il envoie une requête ARP pour résoudre l'adresse IP de l'appareil de destination en son adresse MAC. La demande est diffusée à tous les appareils sur le LAN et contient l'adresse IP de l'appareil de destination. L'appareil avec l'adresse IP correspondante répond avec son adresse MAC.

#### Réponse ARP

Lorsqu'un appareil reçoit une requête ARP, il envoie une réponse ARP à l'appareil demandeur avec son adresse MAC. Le message de réponse contient les adresses IP et MAC des appareils demandeurs et répondeurs.

#### Capture Tshark des requêtes ARP

  Capture Tshark des requêtes ARP

```shell-session
1   0.000000 10.129.12.100 -> 10.129.12.255 ARP 60  Who has 10.129.12.101?  Tell 10.129.12.100
2   0.000015 10.129.12.101 -> 10.129.12.100 ARP 60  10.129.12.101 is at AA:AA:AA:AA:AA:AA

3   0.000030 10.129.12.102 -> 10.129.12.255 ARP 60  Who has 10.129.12.103?  Tell 10.129.12.102
4   0.000045 10.129.12.103 -> 10.129.12.102 ARP 60  10.129.12.103 is at BB:BB:BB:BB:BB:BB
```

Le `who has`message " " dans les première et troisième lignes indique qu'un appareil demande l'adresse MAC pour l'adresse IP spécifiée, tandis que les deuxième et quatrième lignes affichent la réponse ARP avec l'adresse MAC de l'appareil de destination.

Cependant, il est également vulnérable aux attaques, telles que [ARP Spoofing](https://en.wikipedia.org/wiki/ARP_spoofing) , qui peuvent être utilisées pour intercepter ou manipuler le trafic sur le réseau. Cependant, pour se protéger contre de telles attaques, il est important de mettre en place des mesures de sécurité telles que des pare-feux et des systèmes de détection d'intrusion.

`ARP spoofing`, également connu sous le nom de `ARP cache poisoning` ou `ARP poison routing`, est une attaque qui peut être effectuée à l'aide d'outils tels que [Ettercap](https://github.com/Ettercap/ettercap) ou [Cain & Abel](https://github.com/xchwarze/Cain) dans lesquels nous envoyons des messages ARP falsifiés sur un réseau local. L'objectif est d'associer notre adresse MAC à l'adresse IP d'un appareil légitime sur le réseau de l'entreprise, ce qui nous permet effectivement d'intercepter le trafic destiné à l'appareil légitime. Par exemple, cela pourrait ressembler à ce qui suit :

  Capture Tshark des requêtes ARP

```shell-session
1   0.000000 10.129.12.100 -> 10.129.12.101 ARP 60  10.129.12.100 is at AA:AA:AA:AA:AA:AA
2   0.000015 10.129.12.100 -> 10.129.12.255 ARP 60  Who has 10.129.12.101?  Tell 10.129.12.100
3   0.000030 10.129.12.101 -> 10.129.12.100 ARP 60  10.129.12.101 is at BB:BB:BB:BB:BB:BB
4   0.000045 10.129.12.100 -> 10.129.12.101 ARP 60  10.129.12.100 is at AA:AA:AA:AA:AA:AA
```

Les première et quatrième lignes nous montrent ( `10.129.12.100`) l'envoi de messages ARP falsifiés à la cible, associant son adresse MAC à son adresse IP ( `10.129.12.101`). Les deuxième et troisième lignes montrent que la cible envoie une requête ARP et répond à notre adresse MAC. Cela indique que nous avons empoisonné le cache ARP de la cible et que tout le trafic destiné à la cible sera désormais envoyé à notre adresse MAC.

Nous pouvons utiliser l'empoisonnement ARP pour effectuer diverses activités, telles que voler des informations sensibles, rediriger le trafic ou lancer des attaques MITM. Cependant, pour se protéger contre l'usurpation ARP, il est important d'utiliser des protocoles réseau sécurisés, tels que IPSec ou SSL, et de mettre en œuvre des mesures de sécurité, telles que des pare-feu et des systèmes de détection d'intrusion.

