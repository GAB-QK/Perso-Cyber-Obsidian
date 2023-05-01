---
id: CUPP
created_date: 28/10/2022
updated_date: 28/10/2022
type: note
---

#  CUPP
- **🏷️Tags** :  #10-2022 

## 📝 Notes

De nombreux outils peuvent créer une liste de mots de passe personnalisée en fonction de certaines informations. L'outil que nous allons utiliser est `cupp`, qui est pré-installé dans votre PwnBox. Si nous faisons l'exercice à partir de notre propre machine virtuelle, nous pouvons l'installer avec `sudo apt install cupp`ou le cloner à partir du [référentiel Github](https://github.com/Mebus/cupp) . `Cupp`est très facile à utiliser. Nous l'exécutons en mode interactif en spécifiant l' `-i`argument, et répondons aux questions, comme suit :

```shell-session
GabrielQK@htb[/htb]$ cupp -i

___________
   cupp.py!                 # Common
      \                     # User
       \   ,__,             # Passwords
        \  (oo)____         # Profiler
           (__)    )\
              ||--|| *      [ Muris Kurgas | j0rgan@remote-exploit.org ]
                            [ Mebus | https://github.com/Mebus/]


[+] Insert the information about the victim to make a dictionary
[+] If you don't know all the info, just hit enter when asked! ;)

> First Name: William
> Surname: Gates
> Nickname: Bill
> Birthdate (DDMMYYYY): 28101955

> Partners) name: Melinda
> Partners) nickname: Ann
> Partners) birthdate (DDMMYYYY): 15081964

> Child's name: Jennifer
> Child's nickname: Jenn
> Child's birthdate (DDMMYYYY): 26041996

> Pet's name: Nila
> Company name: Microsoft

> Do you want to add some key words about the victim? Y/[N]: Phoebe,Rory
> Do you want to add special chars at the end of words? Y/[N]: y
> Do you want to add some random numbers at the end of words? Y/[N]:y
> Leet mode? (i.e. leet = 1337) Y/[N]: y

[+] Now making a dictionary...
[+] Sorting list and removing duplicates...
[+] Saving dictionary to william.txt, counting 43368 words.
[+] Now load your pistolero with william.txt and shoot! Good luck!
```


## Questions/Thoughts


## 🔗 Links
- 