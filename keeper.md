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

On a donc un système d'authentification Usernam paswd.





## Questions/Thoughts


## 🔗 Links
- 