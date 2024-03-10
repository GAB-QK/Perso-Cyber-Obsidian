---
id: python
created_date: 07/12/2023
updated_date: 07/12/2023
type: note
---

#  python
- **🏷️Tags** :  #12-2023 #python #courses #mac_adresse #cyber #scripting 

## 📝 Codes

### Mac changer 

```python
#!/usr/bin/env python

import subprocess
import optparse

  

def get_arguments():
	
	# Création d'un objet OptionParser pour gérer les arguments en ligne de commande
	parser = optparse.OptionParser()
	parser.add_option("-i", "--interface", dest="interface", help="Interface to change MAC address")
	parser.add_option("-m", "--mac", dest="new_mac", help="New MAC address")
	# Analyse des arguments passés en ligne de commande
	(options, arguments) = parser.parse_args()

	# Vérification de la présence de l'option "interface" et "new_mac"
	if not options.interface:
	parser.error("[-] Please specify an interface, use --help for more info.")	
	elif not options.new_mac:
	parser.error("[-] Please specify a new MAC, use --help for more info.")
	return options
  

def change_mac(interface, new_mac):
	print("[+] Changing MAC address for " + interface + " to " + new_mac)
	# Mise de l'interface réseau en mode "down"
	subprocess.call(["ifconfig", interface, "down"])
	# Changement de l'adresse MAC de l'interface réseau
	subprocess.call(["ifconfig", interface, "hw", "ether", new_mac])
	# Mise de l'interface réseau en mode "up"
	subprocess.call(["ifconfig", interface, "up"])

  

# Récupération des arguments en ligne de commande
options = get_arguments()
change_mac(options.interface, options.new_mac)
```

### Check mac change

```python
#!/usr/bin/env python

import subprocess
import optparse
import re
  

def get_arguments():
	
	# Création d'un objet OptionParser pour gérer les arguments en ligne de commande
	parser = optparse.OptionParser()
	parser.add_option("-i", "--interface", dest="interface", help="Interface to change MAC address")
	parser.add_option("-m", "--mac", dest="new_mac", help="New MAC address")
	# Analyse des arguments passés en ligne de commande
	(options, arguments) = parser.parse_args()

	# Vérification de la présence de l'option "interface" et "new_mac"
	if not options.interface:
	parser.error("[-] Please specify an interface, use --help for more info.")	
	elif not options.new_mac:
	parser.error("[-] Please specify a new MAC, use --help for more info.")
	return options


def change_mac(interface, new_mac):
	print("[+] Changing MAC address for " + interface + " to " + new_mac)
	# Mise de l'interface réseau en mode "down"
	subprocess.call(["ifconfig", interface, "down"])
	# Changement de l'adresse MAC de l'interface réseau
	subprocess.call(["ifconfig", interface, "hw", "ether", new_mac])
	# Mise de l'interface réseau en mode "up"
	subprocess.call(["ifconfig", interface, "up"])

def get_current_mac(interface):

	ifconfig_result = subprocess.check_output(["ifconfig", interface])
	# Utilisation de la méthode "decode" pour convertir le résultat de la commande "ifconfig" en chaine de caractères
	mac_address_search_result = re.search(r"\w\w:\w\w:\w\w:\w\w:\w\w:\w\w", ifconfig_result.decode())
	# Vérification de la présence d'une adresse MAC
	if mac_address_search_result:
	return mac_address_search_result.group(0) # .group(0) permet de retourner le resultat exact de la recherche
	else:
	print("[-] Could not read MAC address.")

# Récupération des arguments en ligne de commande
options = get_arguments()

current_mac = get_current_mac(options.interface)
print("Current MAC = " + str(current_mac))

# Appel de la fonction pour changer l'adresse MAC
change_mac(options.interface, options.new_mac)

current_mac = get_current_mac(options.interface)
	if current_mac == options.new_mac:
		print("[+] MAC address was successfully changed to " + current_mac)
	else:
		print("[-] MAC address did not get changed.")
