---
id: Network
created_date: 29/04/2023
updated_date: 29/04/2023
type: note
---

#  Network
- **🏷️Tags** :  #04-2023 #Network #basics #Proxies

## 📝 Notes

## Sous-réseau IP

---

La division d'une plage d'adresses d'adresses IPv4 en plusieurs plages d'adresses plus petites est appelée `subnetting`.

Un sous-réseau est un segment logique d'un réseau qui utilise des adresses IP avec la même adresse réseau. Nous pouvons considérer un sous-réseau comme une entrée étiquetée sur un grand couloir de bâtiment. Par exemple, il peut s'agir d'une porte vitrée qui sépare les différents départements d'un bâtiment d'entreprise. Avec l'aide du sous-réseau, nous pouvons créer nous-mêmes un sous-réseau spécifique ou découvrir le schéma suivant du réseau respectif :

-   `Network address`
-   `Broadcast address`
-   `First host`
-   `Last host`
-   `Number of hosts`

Prenons comme exemple l'adresse IPv4 et le masque de sous-réseau suivants :

-   Adresse IPv4 :`192.168.12.160`
-   Masque de sous-réseau :`255.255.255.192`
-   CIDR :`192.168.12.160/26`

---

Nous savons déjà qu'une adresse IP est divisée en `network part` et en `host part`.

| Partie réseau         | 1er octet | 2e octet | 3e octet | 4e octet | Décimal           |
|-----------------------|----------|----------|----------|----------|-------------------|
| IPv4                  | **1100 0000**| **1010 1000**| **0000 1100**| **10**10 0000| 192.168.12.160**/26** |
| Masque de sous-réseau | **1111 1111**| **1111 1111**| **1111 1111**| **11**00 0000| **255.255.255.192**   |
| Morceaux              | /8       | /16      | /24      | /32      |                   |

Dans le sous-réseau, nous utilisons le masque de sous-réseau comme modèle pour l'adresse IPv4. À partir des `1`-bits du masque de sous-réseau, nous savons quels bits de l'adresse IPv4 ne doivent pas être modifiés. Ce sont fixe et déterminent donc le "réseau principal" dans lequel se trouve le sous-réseau.

| Partie hôte         | 1er octet | 2e octet | 3e octet | 4e octet | Décimal           |
|-----------------------|----------|----------|----------|----------|-------------------|
| IPv4                  | 1100 0000| 1010 1000| 0000 1100| 10**10 0000**| 192.168.12.160/26 |
| Masque de sous-réseau | 1111 1111| 1111 1111| 1111 1111| 11**00 0000**| 255.255.255.192   |
| Morceaux              | /8       | /16      | /24      | /32      |                   |

Les bits dans `host part` peuvent être remplacés par l' adresse `first` et `last`. La première adresse est le `network address`, et la dernière adresse est le `broadcast address` pour le sous-réseau respectif.

>Le `network address` est vital pour la livraison d'un paquet de données. Si le `network address` est le même pour l'adresse source et de destination, le paquet de données est livré dans le même sous-réseau. Si les adresses réseau sont différentes, le paquet de données doit être acheminé vers un autre sous-réseau via le `default gateway`.

Le `subnet mask` détermine où cette séparation se produit.

| Partie hôte         | 1er octet | 2e octet | 3e octet | 4e octet | Décimal           |
|-----------------------|----------|----------|----------|----------|-------------------|
| IPv4                  | 1100 0000| 1010 1000| 0000 1100| 1010 0000| 192.168.12.160 **/26** |
| Masque de sous-réseau | **1111 1111**| **1111 1111**| **1111 1111**| **11**00 0000| 255.255.255.192   |
| Morceaux              | /8       | /16      | /24      | /32      |                   |

#### Adresse réseau

Donc, si nous définissons maintenant tous les bits sur `0` dans `host part`l'adresse IPv4, nous obtenons le sous-réseau respectif `network address`.

| Partie réseau         | 1er octet | 2e octet | 3e octet | 4e octet | Décimal           |
|-----------------------|----------|----------|----------|----------|-------------------|
| IPv4                  | 1100 0000| 1010 1000| 0000 1100| 10 **00 0000**| **192.168.12.128**/26 |
| Masque de sous-réseau | **1111 1111**| **1111 1111**| **1111 1111**| **11**00 0000| 255.255.255.192   |
| Morceaux              | /8       | /16      | /24      | /32      |                   |

---

#### Adresse de diffusion

Si nous définissons tous les bits de `host part`l'adresse IPv4 sur `1`, nous obtenons le `broadcast address`.

| Partie réseau         | 1er octet | 2e octet | 3e octet | 4e octet | Décimal           |
|-----------------------|----------|----------|----------|----------|-------------------|
| IPv4                  | 1100 0000| 1010 1000| 0000 1100| 10 **11 1111**| **192.168.12.191**/26 |
| Masque de sous-réseau | **1111 1111**| **1111 1111**| **1111 1111**| **11**00 0000| 255.255.255.192   |
| Morceaux              | /8       | /16      | /24      | /32      |                   |

Comme nous savons maintenant que les adresses IPv4 `192.168.12.128` et `192.168.12.191` sont attribuées, toutes les autres adresses IPv4 sont donc comprises entre `192.168.12.129-190`. Nous savons maintenant que ce sous-réseau nous offre un total de `64 - 2` (adresse réseau et adresse de diffusion) ou `62` d'adresses IPv4 que nous pouvons attribuer à nos hôtes.

| Hôtes         | IPv4            |
| ------------- | --------------- |
| Adresse réseau | 192.168.12.128  |
| Premier hôte   | 192.168.12.129  |
| Autres hôtes   | ...             |
| Dernier hôte   | 192.168.12.190  |
| Adresse de diffusion | 192.168.12.191 |

---

## Création de sous-réseaux dans des réseaux plus petits

Supposons maintenant que nous, en tant qu'administrateurs, avons été chargés de diviser le sous-réseau qui nous est attribué en 4 sous-réseaux supplémentaires. Ainsi, il est essentiel de savoir que nous ne pouvons diviser les sous-réseaux qu'en fonction du système binaire.

| Exposant | Valeur |
| --------|-------|
| 2^0     |   1   |
| 2^1     |   2   |
| 2^2     |   4   |
| 2^3     |   8   |
| 2^4     |  16   |
| 2^5     |  32   |
| 2^6     |  64   |
| 2^7     |  128  |
| 2^8     |  256  |

---

Par conséquent, nous pouvons diviser le que `64 hosts`nous connaissons par `4`. Le `4`est égal à l'exposant 2 `^2`dans le système binaire, nous trouvons donc le nombre de bits du masque de sous-réseau par lequel nous devons l'étendre. Nous connaissons donc les paramètres suivants :

-   Sous-réseau :`192.168.12.128/26`
-   Sous-réseaux requis :`4`

Maintenant, nous augmentons/développons notre masque de sous-réseau de `2 bits`de `/26` à `/28`, et il ressemble à ceci :

| Partie réseau         | 1er octet | 2e octet | 3e octet | 4e octet | Décimal           |
|-----------------------|----------|----------|----------|----------|-------------------|
| IPv4                  | 1100 0000| 1010 1000| 0000 1100| 1011 1111| 192.168.12.191/**28** |
| Masque de sous-réseau | **1111 1111**| **1111 1111**| **1111 1111**| **1111** 0000| **255.255.255.240**   |
| Morceaux              | /8       | /16      | /24      | /32      |                   |

Ensuite, nous pouvons diviser les `64` adresses IPv4 qui nous sont disponibles en `4 parts`:

| Hôtes | Mathématiques | Sous-réseaux | Plage d'hôtes pour chaque sous-réseau |
|-------|--------------|--------------|--------------------------------------|
| 64    | /            | 4            | =16                                  |

Nous savons donc quelle sera la taille de chaque sous-réseau. A partir de maintenant, on part de l'adresse réseau qui nous est donnée (192.168.12.128) et on ajoute les heures `16` des hosts : `4`

| N° de sous-réseau | Adresse réseau    | Premier hôte     | Dernier hôte     | Adresse de diffusion | CIDR            |
|------------------|-------------------|------------------|------------------|----------------------|-----------------|
| 1                | 192.168.12.128    | 192.168.12.129  | 192.168.12.142  | 192.168.12.143         | 192.168.12.128/28 |
| 2                | 192.168.12.144    | 192.168.12.145  | 192.168.12.158  | 192.168.12.159         | 192.168.12.144/28 |
| 3                | 192.168.12.160    | 192.168.12.161  | 192.168.12.174  | 192.168.12.175         | 192.168.12.160/28 |
| 4                | 192.168.12.176    | 192.168.12.177  | 192.168.12.190  | 192.168.12.191         | 192.168.12.176/28 |

---

## Sous-réseau mental

>[!info]
>Il peut sembler qu'il y ait beaucoup de calculs impliqués dans la création de sous-réseaux, mais chaque octet se répète, et tout est une puissance de deux, donc il n'est pas nécessaire d'avoir beaucoup de mémorisation. La première chose à faire est d'identifier quel octet change.


Il est possible d'identifier quel octet de l'adresse IP peut changer en se souvenant de ces quatre chiffres. Étant donné l'adresse réseau : `192.168.1.1/25`, il est immédiatement évident que 192.168.2.4 ne serait pas dans le même réseau car le `/25` sous-réseau signifie que seul le quatrième octet peut changer.

La partie suivante identifie la taille de chaque sous-réseau, mais en divisant huit par le réseau et en examinant le fichier `remainder`. Ceci est également appelé `Modulo Operation (%)` et est fortement utilisé en cryptologie. Étant donné notre exemple précédent de `/25`, `(25 % 8)` serait 1. C'est parce que huit va dans 25 trois fois (8 * 3 = 24). Il reste un 1, qui est le bit de réseau réservé au masque de réseau. Il y a un total de huit bits dans chaque octet d'une adresse IP. Si l'on en utilise un pour le masque de réseau, l'équation devient 2^(8-1) ou 2^7, 128. Le tableau ci-dessous contient tous les nombres.

| Reste | Nombre | Forme exponentielle | Formulaire de division |
|-------|--------|---------------------|------------------------|
| 0     | 256    | 2^8                 | 256                    |
| 1     | 128    | 2^7                 | 256/2                  |
| 2     | 64     | 2^6                 | 256/2/2                |
| 3     | 32     | 2^5                 | 256/2/2/2              |
| 4     | 16     | 2^4                 | 256/2/2/2/2            |
| 5     | 8      | 2^3                 | 256/2/2/2/2/2          |
| 6     | 4      | 2^2                 | 256/2/2/2/2/2/2        |
| 7     | 2      | 2^1                 | 256/2/2/2/2/2/2/2      |

En se souvenant des puissances de deux à huit, cela peut devenir un calcul instantané. Cependant, s'il est oublié, il peut être plus rapide de se souvenir de diviser 256 par la moitié du nombre de fois du reste.

La partie la plus délicate consiste à obtenir la plage d'adresses IP réelle, car 0 est un nombre et non nul dans le réseau. Ainsi, dans notre `/25` avec 128 adresses IP, la première plage est `192.168.1.0-127`. La première adresse est le réseau et la dernière est l'adresse de diffusion, ce qui signifie que l'espace IP utilisable deviendrait `192.168.1.1-126`. Si notre adresse IP dépassait 128, alors ce `usable ip space` serait 192.168.129-254 (128 IPs le réseau et 255 est la diffusion).