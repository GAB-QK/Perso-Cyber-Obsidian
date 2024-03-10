---
id: SAU
created_date: 03/11/2023
updated_date: 03/11/2023
type: note
---

#  SAU
- **🏷️Tags** :  #11-2023 

## 📝 Notes

### Nmap

![[Pasted image 20231103112616.png | 1000]]

### Exploration du Port 55555
![[Pasted image 20231103112723.png]]

>[!Note] 
>gsosrc9

![[Pasted image 20231103112833.png]]

>[!tip] Tip
> création du basket et nous fournis un token
> `8Ke6Rk0jR5A3KroAbT6PbrRZxKOWQ0ZOBTQ90f-9ED1d`
> 
> accéder au bask avec le token : 
> http://10.10.11.224:55555/web/gsosrc9?token=8Ke6Rk0jR5A3KroAbT6PbrRZxKOWQ0ZOBTQ90f-9ED1d

```python
import requests  

url = "http://10.10.11.224:55555/gab"
#ajoute un body à la requête
body = {"name": "Gabriel", "age": 23}
#ajoute un header à la requête
headers = {"Content-Type": "application/json"}
#envoie la requête
response = requests.post(url, json=body, headers=headers)

if response.status_code == 200:
	print("Requête réussie !")
	print("Contenu de la réponse:")
	print(response.text)
else :
	print(f"erreur {response.status_code}")
```

On récupère des réponses sur le site :
![[Pasted image 20231103115629.png]]

On s’aperçoit aussi de la version utilisé du service qui tourne sur ce site

![[Pasted image 20231103122653.png | 1000]]

En faisant quelques recherches on trouve un exploit sur ce service et cette version
[Vulners](https://vulners.com/packetstorm/PACKETSTORM:174128)

![[Pasted image 20231103122932.png | 1000]]



## Questions/Thoughts


## 🔗 Links
- 