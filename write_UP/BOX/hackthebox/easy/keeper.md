---
id: keeper
created_date: 29/10/2023
updated_date: 29/10/2023
type: note
tags:
  - writeup
  - easy
  - keepass
  - ssh
  - dfsg_debian
---

#  keeper
- **🏷️Tags** :  #10-2023 #writeup #easy #keepass #ssh #dfsg_debian

## 📝 Notes

# reconnaissance 

Dans un premier temps on regarde les ports qui sont ouverts sur la machine cible


```bash
nmap -sC -sV 10.0.0.1

Nmap scan report for 10.10.11.227
Host is up (0.025s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 3539d439404b1f6186dd7c37bb4b989e (ECDSA)
|_  256 1ae972be8bb105d5effedd80d8efc066 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: nginx/1.18.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

On observe donc qu'il y a dans un premier temps le port 22 du port ssh d'ouvert et le port 80 pour le protocole http

On se rend donc sur notre browser fav aka Vivaldi avec l'adresse IP et le port adéquat.

![[Pasted image 20231029140911.png]]

On a donc un système d'authentification Username password.

> On récupère une information importante sur cette page d'authentification. En effet la version utiliser 4.4.4 dfsg 2ubuntu1 , on va donc regarder sur l'internet les logins par default utilisé, avec un peu de chance ça peut passer.

![[Drawing 2023-11-01 19.08.56.excalidraw]]


En cherchant on trouve que les identifiants par defaults son root/password.

Cela nous donne accès au site web, une fois cela fait on commence à farfouiller sur le site. On tombe sur des users, en cliquant dessus on se rend compte qu'on nous donne les informations de connections dans les notes du profil.

![[Pasted image 20231101192548.png]]

# Infiltration du User 

On sait que le port SSH est ouvert grace au scan de ports qu'on a effectué au début. On peut donc tenter de se connecter en ssh avec ce profil.

![[Pasted image 20231101192919.png]]

>[!Success] Bravo
>On récupère donc le premier flag user.

# Root

En ce qui concerne l'utilisateur root, on remarque la présence de nombreux fichier.

![[Pasted image 20231101193115.png]]

On peut rapidement en déduire qu'il sagit d'une fuite de keepass. en cherchant le nom des fichiers sur internet on s'aperçoit de l’existence d'une vulnérabilité qui touche keepass, la **CVE-2023-32784**

![[Pasted image 20231101193628.png]]

>En se rendant sur le git on trouve script qui permet de dumper la mémoire du fichier et de récupérer le mdp.

On execute le script et boum on récupère un semblant de mdp, pour le récupérer entier on utilise tout simplement google. en cherchant le dernier résultat on obtient un dessert danois qui se nomme "rødgrød med fløde"

![[Pasted image 20231101194023.png]]

On arrive donc à ouvrir le wallet keepass et récuperer les mdp.

# Keepass

Sur keepass on observe que le user root est présent et avec le mdp F4><3K0nd!

![[Pasted image 20231101195813.png]]

cependant cela ne va pas fonctionner. Mais on observe dans les notes la présence d'une clé ssh-rsa. On va donc l'utiliser.

Pour cela on va utilise la commande suivant :

```bash
puttygen keeper.txt -O private-openssh -o id_rsa
```

>[!warning] Attention
>le fichier keeper est juste le texte présente dans la note du keepass avec la clé RSA on la transforme juste en clé valide

ensuite il suffit de se connecter directement en ssh en précisant bien la clé RSA.


```bash
ssh root@10.10.10.10 -i id_rsa
```

On récupère ensuite le flag root.
## Questions/Thoughts


## 🔗 Links
- 