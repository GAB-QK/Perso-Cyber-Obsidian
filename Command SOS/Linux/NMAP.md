---
id: NMAP
created_date: 17/04/2023
updated_date: 17/04/2023
type: note
---

#  NMAP
- **🏷️Tags** :  #04-2023 

## 📝 Notes

## Scanning Options

  

| **Nmap Option** | **Description** |
|---|----|
| `10.10.10.0/24` | Target network range. |
| `-sn` | Disables port scanning. |
| `-Pn` | Disables ICMP Echo Requests |
| `-n` | Disables DNS Resolution. |
| `-PE` | Performs the ping scan by using ICMP Echo Requests against the target. |
| `--packet-trace` | Shows all packets sent and received. |
| `--reason` | Displays the reason for a specific result. |
| `--disable-arp-ping` | Disables ARP Ping Requests. |
| `--top-ports=<num>` | Scans the specified top ports that have been defined as most frequent. |
| `-p-` | Scan all ports. |
| `-p22-110` | Scan all ports between 22 and 110. |
| `-p22,25` | Scans only the specified ports 22 and 25. |
| `-F` | Scans top 100 ports. |
| `-sS` | Performs an TCP SYN-Scan. |
| `-sA` | Performs an TCP ACK-Scan. |
| `-sU` | Performs an UDP Scan. |
| `-sV` | Scans the discovered services for their versions. |
| `-sC` | Perform a Script Scan with scripts that are categorized as "default". |
| `--script <script>` | Performs a Script Scan by using the specified scripts. |
| `-O` | Performs an OS Detection Scan to determine the OS of the target. |
| `-A` | Performs OS Detection, Service Detection, and traceroute scans. |
| `-D RND:5` | Sets the number of random Decoys that will be used to scan the target. |
| `-e` | Specifies the network interface that is used for the scan. |
| `-S 10.10.10.200` | Specifies the source IP address for the scan. |
| `-g` | Specifies the source port for the scan. |
| `--dns-server <ns>` | DNS resolution is performed by using a specified name server. |

  
## Output Options


| **Nmap Option** | **Description**                                                                   |
| --------------- | --------------------------------------------------------------------------------- |
| `-oA filename`  | Stores the results in all available formats starting with the name of "filename". |
| `-oN filename`  | Stores the results in normal format with the name "filename".                     |
| `-oG filename`  | Stores the results in "grepable" format with the name of "filename".              |
| `-oX filename`  | Stores the results in XML format with the name of "filename".                     |
| `xsltproc target.xml -o target.html` | permet de convertir le fichier xml en format html            |

## # Firewall and IDS/IPS Evasion Exemple

La méthode d'analyse TCP ACK ( ) de Nmap `-sA`est beaucoup plus difficile à filtrer pour les pare-feux et les systèmes IDS/IPS que `-sS`les analyses SYN ( ) ou Connect ( `sT`) classiques car elles n'envoient qu'un paquet TCP avec uniquement le `ACK`drapeau. Lorsqu'un port est fermé ou ouvert, l'hôte doit répondre par un `RST`indicateur. Contrairement aux connexions sortantes, toutes les tentatives de connexion (avec le `SYN`drapeau) à partir de réseaux externes sont généralement bloquées par des pare-feu. Cependant, les paquets avec l' `ACK`indicateur sont souvent passés par le pare-feu car le pare-feu ne peut pas déterminer si la connexion a d'abord été établie à partir du réseau externe ou du réseau interne.

### SYN-Scan

```shell-session
sudo nmap 10.129.2.28 -p 21,22,25 -sS -Pn -n --disable-arp-ping --packet-trace
```

### ACK-Scan

```shell-session
sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace
```


### Numérisation à l'aide de leurres

```shell-session
sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5
```

### Test de règle des pare-feu

```shell-session
sudo nmap 10.129.2.28 -n -Pn -p445 -O
```

### Analyser en utilisant une adresse IP source différente

```shell-session
sudo nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0
```

### SYN-Scan d'un port filtré

```shell-session
sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace
```

### SYN-Scan depuis le port DNS

```shell-session
sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53
```

### Connectez-vous au port filtré

```shell-session
ncat -nv --source-port 53 10.129.2.28 50000
```


## Performance Options

| **Nmap Option** | **Description** |
|---|----|
| `--max-retries <num>` | Sets the number of retries for scans of specific ports. |
| `--stats-every=5s` | Displays scan's status every 5 seconds. |
| `-v/-vv` | Displays verbose output during the scan. |
| `--initial-rtt-timeout 50ms` | Sets the specified time value as initial RTT timeout. |
| `--max-rtt-timeout 100ms` | Sets the specified time value as maximum RTT timeout. |
| `--min-rate 300` | Sets the number of packets that will be sent simultaneously. |
| `-T <0-5>` | Specifies the specific timing template. |

## Questions/Thoughts


## 🔗 Links
- 