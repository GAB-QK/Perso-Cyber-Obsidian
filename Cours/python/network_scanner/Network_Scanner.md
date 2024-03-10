---
id: Network_Scanner
created_date: 08/12/2023
updated_date: 08/12/2023
type: note
---

#  Network_Scanner
- **🏷️Tags** :  #12-2023 #python #courses  #cyber #Network #scan #scripting 

## 📝 Codes


```python
#!/usr/bin/env python

import scapy.all as scapy
import optparse

def get_arguments():
	parser = optparse.OptionParser()
	parser.add_option("-t", "--target", dest="target", help="Target IP / IP range.")
	(options, arguments) = parser.parse_args()
	
	if not options.target:
		parser.error("[-] Please specify a target, use --help for more info.")
	return options

def scan(ip):
	arp_request = scapy.ARP(pdst=ip)
	broadcast = scapy.Ether(dst="ff:ff:ff:ff:ff:ff")
	arp_request_broadcast = broadcast/arp_request # Création d'un objet ARP sur le réseau local
	answered_list = scapy.srp(arp_request_broadcast, timeout=1, verbose=False)[0]
	
	client_list = []
	for element in answered_list:
		client_dict = {"ip": element[1].psrc, "mac": element[1].hwsrc} # psrc = IP source, hwsrc = MAC source
		client_list.append(client_dict)
	return client_list

def print_result(results_list):
	print("IP\t\t\tMAC Address\n-----------------------------------------")
	for client in results_list:
		print(client["ip"] + "\t\t" + client["mac"])

  

options = get_arguments()

print_result(scan(options.target))
```


## Questions/Thoughts


## 🔗 Links
- 