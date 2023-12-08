---
id: Beautifulsoup
created_date: 03/05/2023
updated_date: 03/05/2023
type: note
---

#  Beautifulsoup
- **🏷️Tags** :  #05-2023 #python  #librairies

## 📝 Notes

# Utilisation de BeautifulSoup en Python

BeautifulSoup est une bibliothèque Python qui permet de traiter des documents HTML et XML. Elle fournit des outils pour extraire et manipuler des données à partir de ces types de fichiers. Voici les étapes de base pour utiliser BeautifulSoup :

## Étape 1: Installation

Pour installer BeautifulSoup, vous pouvez utiliser pip, le gestionnaire de packages de Python :

Copy code      


```python
pip install beautifulsoup4
```


## Étape 2: Importation

Vous devez importer la bibliothèque BeautifulSoup dans votre code Python pour l'utiliser :



``` python
from bs4 import BeautifulSoup
```


## Étape 3: Récupération du contenu HTML

Pour utiliser BeautifulSoup, vous devez récupérer le contenu HTML de la page Web que vous souhaitez analyser. Cela peut être fait en utilisant la bibliothèque de requêtes :



```python
import requests 
import bs4 from BeautifulSoup

session = requests.Session()
login_link = "https://github.com/SeenKid/flipper-zero-bad-usb"
response = session.get(login_link)
soup = BeautifulSoup(response.content, "html.parser")

```

## Étape 4: Navigation dans le contenu

Une fois que vous avez récupéré le contenu HTML, vous pouvez naviguer à travers lui en utilisant les méthodes de BeautifulSoup pour trouver des éléments spécifiques ou extraire du texte :



```python
# Trouver le titre de la page
title = soup.title.string 
# Trouver tous les liens sur la page
links = soup.find_all('a') 
# Extraire le texte de la balise <p> 
paragraphs = soup.find_all('p') 
text = [p.get_text() for p in paragraphs]
```


## Conclusion

Voilà! C'est un aperçu rapide de l'utilisation de BeautifulSoup en Python. Avec ces étapes de base, vous pouvez commencer à extraire et manipuler des données à partir de fichiers HTML et XML.


## Utilisation avec un Webhook discord

>[!warning]
>voir le Tuto Webhook discord avant 

```python
import requests
from bs4 import BeautifulSoup

# Discord webhook URL

webhook_url = "webhook_link"

# session publique git

session = requests.Session()
link = "https://github.com/SeenKid/flipper-zero-bad-usb"
response = session.get(link)
soup = BeautifulSoup(response.content, "html.parser")
depot_file_names = soup.find_all("span", {"class": "css-truncate css-truncate-target d-block width-fit"})

  
# Create the Discord message with your liked tweets

discord_message = "les données scrap par bs4:\n\n"
for depot_file_name in depot_file_names:
text = depot_file_name.text
discord_message += f"- {text}\n\n"

# Send the message to your Discord server

payload = {"content": discord_message}
headers = {"Content-Type": "application/json"}
response = requests.post(webhook_url, json=payload, headers=headers)
```

>[!résultat]
>On reçoit donc sur notre serveur discord le résultat suivant 

![[Pasted image 20230503133033.png]]

