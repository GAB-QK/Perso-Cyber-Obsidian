---
id: Network
created_date: 29/04/2023
updated_date: 29/04/2023
type: note
---

#  Network
- **🏷️Tags** :  #04-2023 #Network #basics #networkTypes

## 📝 Notes

## Types de réseaux

Chaque réseau est structuré différemment et peut être configuré individuellement. Pour cette raison, des types et des topologies appelés « types de réseaux » ont été développés pour catégoriser ces réseaux. La lecture de tous les types de réseaux peut être une surcharge d'informations car certains types de réseaux incluent la portée géographique. Nous entendons rarement certaines terminologies en pratique, donc cette section sera divisée en termes courants et termes de livre. Les termes de livre sont bons à connaître, car il y a eu un seul cas documenté d'un serveur de messagerie électronique ne parvenant pas à livrer des e-mails de plus de 500 miles, mais ne vous attendez pas à pouvoir les réciter sur demande à moins que vous ne passiez un examen de réseau.

## Terminologie courante

| Type de réseau | Définition |
| --- | --- |
| WAN | Internet |
| LAN | Réseaux internes (par exemple, à domicile ou au bureau) |
| WLAN | Réseaux internes accessibles via Wi-Fi |
| VPN | Connecte plusieurs sites de réseau à un seul LAN |

### WAN

Le WAN (Wide Area Network) est communément appelé l'Internet. Lorsque l'on travaille avec du matériel de réseau, nous avons souvent une adresse WAN et une adresse LAN. Le WAN est l'adresse généralement accessible par Internet. Cela dit, cela ne se limite pas à Internet; un WAN est simplement un grand nombre de LAN joints ensemble. De nombreuses grandes entreprises ou agences gouvernementales auront un "WAN interne" (également appelé Intranet, réseau à air, etc.). En règle générale, la façon dont nous identifions si le réseau est un WAN est d'utiliser un protocole de routage spécifique au WAN tel que BGP et si le schéma IP utilisé n'est pas conforme à la RFC 1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16).

### LAN / WLAN

Les LAN (réseaux locaux) et WLAN (réseaux locaux sans fil) attribueront généralement des adresses IP désignées pour une utilisation locale (RFC 1918, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16). Dans certains cas, comme certains collèges ou hôtels, vous pouvez vous voir attribuer une adresse IP routable (Internet) en rejoignant leur LAN, mais c'est beaucoup moins courant. Il n'y a rien de différent entre un LAN ou un WLAN, autre que les WLAN introduisent la possibilité de transmettre des données sans câbles. C'est principalement une désignation de sécurité.

### VPN

Il existe trois principaux types de réseaux privés virtuels (VPN), mais les trois ont le même objectif de faire sentir à l'utilisateur comme s'il était connecté à un réseau différent.

#### VPN Site à Site

Les deux clients et serveurs sont des périphériques de réseau, généralement des routeurs ou des pare-feu, et partagent des plages de réseau entières. Ceci est le plus couramment utilisé pour relier des réseaux

#### VPN d'accès à distance

ce type de VPN permet à des utilisateurs individuels de se connecter à distance à un réseau privé en utilisant Internet. Les utilisateurs peuvent accéder aux ressources du réseau privé, telles que des fichiers, des applications et des imprimantes, comme s'ils étaient physiquement présents sur le réseau. Les VPN d'accès distant sont souvent utilisés par des travailleurs à distance ou des voyageurs fréquents qui ont besoin d'accéder à des informations sensibles ou confidentielles.

#### VPN SSL

ce type de VPN est utilisé pour sécuriser les communications entre deux utilisateurs ou deux réseaux privés en utilisant un tunnel crypté. Les VPN de communication sécurisée sont souvent utilisés pour protéger les données sensibles lorsqu'elles sont transmises sur Internet, notamment pour les transactions financières, les informations médicales et les données de cartes de crédit.