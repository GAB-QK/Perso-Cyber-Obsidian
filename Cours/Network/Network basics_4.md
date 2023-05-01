---
id: Network
created_date: 29/04/2023
updated_date: 29/04/2023
type: note
---

#  Network
- **🏷️Tags** :  #04-2023 #Network #basics #Proxies

## 📝 Notes

## Les Proxies : Médiateurs des connexions

Les Proxies sont souvent utilisés pour diverses raisons, mais leur rôle principal est de servir de médiateurs dans les connexions. Cela signifie qu'un appareil ou un service agit comme une sorte de relais entre deux parties de la communication, en examinant le contenu du trafic. Il existe différents types de proxies, chacun ayant ses propres caractéristiques et utilisations.

### Les différentes perceptions des Proxies

Les professionnels de la sécurité ont tendance à associer les Proxies HTTP (comme BurpSuite) ou les Proxies SOCKS/SSH (comme Chisel, ptunnel, sshuttle) à des outils de pivoting. Les développeurs Web utilisent des Proxies tels que Cloudflare ou ModSecurity pour bloquer le trafic malveillant. Pour le grand public, un Proxy est souvent associé à un outil permettant d'accéder à des catalogues Netflix d'autres pays ou de masquer sa localisation. En revanche, pour les forces de l'ordre, les Proxies sont souvent associés à des activités illégales.

>[!info]
Cependant, il convient de rappeler que le rôle principal d'un Proxy est d'agir comme un médiateur dans une connexion.

### Les différents types de Proxies

Les Proxies se situent presque toujours au niveau 7 du modèle OSI. Il existe plusieurs types de Proxies, chacun ayant ses propres caractéristiques et utilisations.

#### Les Dedicated Proxy / Forward Proxy

Le Forward Proxy est le type de Proxy que la plupart des gens imaginent. C'est lorsque le client fait une demande à un ordinateur et que cet ordinateur effectue la demande.

>[!info]
>Dans un réseau d'entreprise, par exemple, des ordinateurs sensibles peuvent ne pas avoir un accès direct à Internet. Pour accéder à un site Web, ils doivent passer par un proxy (ou un filtre Web). Cela peut être une ligne de défense incroyablement puissante contre les logiciels malveillants, car il ne suffit pas de contourner le filtre Web (ce qui est facile), mais il faudrait également être conscient de l'existence d'un Proxy ou utiliser un C2 non traditionnel (une façon pour les logiciels malveillants de recevoir des informations de tâches). Si l'organisation n'utilise que FireFox, il est peu probable que les logiciels malveillants soient conscients de l'existence du Proxy.


![[forward_proxy.png]]


#### Les Reverse Proxy

Le Reverse Proxy, quant à lui, est conçu pour filtrer les demandes entrantes. Le but principal d'un Reverse Proxy est de surveiller une adresse et de la transférer vers un réseau isolé.


>[!info]
>De nombreuses organisations utilisent CloudFlare, qui possède un réseau robuste capable de résister à la plupart des attaques DDoS. En utilisant CloudFlare, les organisations ont un moyen de filtrer la quantité (et le type) de trafic envoyé à leurs serveurs Web.

![[reverse_proxy.png]]

#### Les (non-)Transparent Proxy

Les Proxies peuvent être soit transparents, soit non transparents. Un Proxy transparent intercepte les demandes de communication du client vers Internet et agit comme une instance de substitution. Pour l'extérieur, le Proxy transparent, tout comme le Proxy non transparent, agit comme un partenaire de communication.

>[!info]
>En revanche, pour un Proxy non transparent, nous devons être informés de son existence et de