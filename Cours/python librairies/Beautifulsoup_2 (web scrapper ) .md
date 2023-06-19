---
id: Beautifulsoup
created_date: 03/05/2023
updated_date: 03/05/2023
type: note
---

#  Beautifulsoup
- **🏷️Tags** :  #05-2023 #python  #librairies

## 📝 Notes

# Utilisation de BeautifulSoup avec une session privée

>[!tip]
>Pour récupérer des données d'une session privée cela est un petit peu plus compliqué il va falloir se connecter à la session, prenons l'exemple de git.
>
>Je souhaite ici récupérer les données d'un depot privé mais sans utiliser l'api ( toutes les plateformes ne donnent pas l'accès libre aux API aka twitter qui a une API payante)


```python
import requests
from bs4 import BeautifulSoup

# Discord webhook URL
webhook_url = "https://discord.com/api/webhooks/1103279942524993617/w7gUTw3bREUFIkQ1ZQWv_oQo3wC0HsYfw878TOx7Z0I0fPH76BtpC8rjkHcN6a-HspCA"

  
#create session for login
username = "username"
password = "pwd"
session = requests.Session()

def login(username, password):

	# Envoyer une requête GET pour récupérer le jeton d'authentification CSRF
	login_url = 'https://github.com/session'
	response = session.get(login_url)
	soup = BeautifulSoup(response.content, 'html.parser')
	csrf_token = soup.find('input', {'name': 'authenticity_token'}).get('value')
	  
	# Envoyer une requête POST avec les informations d'identification et le jeton CSRF
	login_data = {
	"commit": "Sign in",
	"authenticity_token": csrf_token,
	"login": username,
	"password": password
	}
	
	# crée une connexion avec les info de login data
	session.post("https://github.com/session", data=login_data)

def web_scrap(session):

	# private git session
	link = "https://github.com/GAB-QK/Cours-Obsidian"
	response = session.get(link)
	soup = BeautifulSoup(response.content, "html.parser")
	depot_file_names = soup.find_all("span", {"class": "css-truncate css-truncate-target d-block width-fit"})
	
	# Create the Discord message with your liked tweets
	discord_message = "les données scrap par bs4:\n\n"
	for depot_file_name in depot_file_names:
	text = depot_file_name.text
	discord_message += f"- {text}\n"
	
	# Send the message to your Discord server
	payload = {"content": discord_message}
	headers = {"Content-Type": "application/json"}
	response = requests.post(webhook_url, json=payload, headers=headers)
	
	def main():
		login(username, password)
		web_scrap(session)
		main()

```
