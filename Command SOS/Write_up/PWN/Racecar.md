---
id: Racecar
created_date: 19/06/2023
updated_date: 19/06/2023
type: note
---

#  Racecar
- **🏷️Tags** :  #06-2023 #buffer #overflow #stack #GDB #reverse #PWN 

### Observation 

Comme pour tout challenge PWN première chose à faire est de regarder quel type de fichier nous est fournie

![[Pasted image 20230619160421.png]]
 - on a donc un binaire que l'on peut exécuter donc exécutons le :
 ![[Pasted image 20230619160708.png]]
 
>[!annotation]
>Le programme se présente de la manière suivante, nous devons dans un premier temps choisir un nom, surnom pour ensuite choisir 2 options les informations sur les voitures et enfin le choix de voiture et de course.
>
>On observe que si l'on choisit la voiture 1 et la course 2 ou bien la voiture 2 et la course 1, alors nous gagnons la course et avons par la suite la possibilité de rentrer un message de victoire.


### Dé-compiler 

- On peut maintenant rentrer dans le vif du sujet et décortiquer le binaire plus en profondeur. Pour cela on utilise le logiciel Ghidra.

- Une fois le fichier ouvert dans le logiciel, on va dans un premier temps regarder les fonctions du programme et plus spécifiquement la fonction **"main()"**.

![[Pasted image 20230619161940.png]]


- On observe donc plusieurs appelle de fonctions ici. En en jetant un coup d’œil rapide on observe une fonction pourrait potentiellement nous intéresser.

![[Pasted image 20230619162234.png]]

>On a ici la fonction **"car_menu()"**, on observe plusieurs choses ici, dans un premier temps on voit apparaître la mention de flag, et dans un second temps on peut observer l'input de victoire à rentrer en cas de victoire.

le **"printf(\_format)"** est une faille connue qui va nous permettre d’accéder à la stack.

>[!Exemple]
> ![[Pasted image 20230619162625.png]]

>[!annotation]
>On observe bien la réponse positif de l'exploit. On a donc peut-être moyen de se balader dans la stack et de retrouver l'adresse du flag et par la même occasions retrouver le flag.

> On va ici se crée un petit script python qui va nous permettre de gagner du temps sur l'exploitation de la faille.


```python
#!/usr/bin/env python3

from pwn import *
from pwn import process
  
def exploit(payload: str):

binary_path='./racecar'
conn = process(binary_path)
conn.sendlineafter(b'Name', b'gabi')
conn.sendlineafter(b'Nickname', b'gabi')
conn.sendlineafter(b'selection', b'2')
conn.sendlineafter(b'car', b'1')
conn.sendlineafter(b'Circuit', b'2')
conn.sendlineafter(b'victory?', bytes(payload, encoding='utf-8'))
conn.recv()
print(conn.recv().decode('utf-8'))
conn.close()  

if __name__ == '__main__':
while True:
exploit(input('Enter payload: '))
```

Cela va nous permettre de tester plus facilement les payloads à injecter dans l'input.

- Avant d’exécuter notre programme nous allons crées un fichier **flag.txt** dans lequel nous allons écrire **"AAA"** ce qui nous donnera quelques chose come 414141 en hexa, ce qui sera plus simple à repérer. 

![[Pasted image 20230619163815.png]]

>[!Resultat]
>On a donc bien une réponse de notre payload injecté, et de plus nous observons l'adresse 0x41414141 à la 12èm position nous avons donc la position de la première adresses du flag. nous pouvons tester cela directement sur le serveur. 

- on récupère donc cette output sur le serveur.

![[Pasted image 20230620121725.png]]


> En passant par le site dcode.com on peut bien voir qu'on récupère bien le flag avec le format **"HTB{}"** que l'on connait.

![[Pasted image 20230620121844.png]]

- Il nous faut maintenant le récupérer dans le bonne ordre. Pour cela on va utiliser un petit script python qui va nous faciliter la tache.c

![[Pasted image 20230620122303.png]]


```python
#!/usr/bin/env python3

import re
raw_flag = input("Enter the raw data: ")
raw_flag = raw_flag.split()[::-1]

for i in range(len(raw_flag)):
	raw_flag[i] = re.findall('..', raw_flag[i])
	print(raw_flag[i])

flag = []
for chars in raw_flag:
	word = ""
	for char in chars[::-1]:
		if char != '0x':
			word += chr(int(char, 16))
	flag.append(word)

flag.reverse()

print(''.join(flag))

```

>[!Success]
>on récupère donc l'output suivant avec le flag dans le bon ordre:
>![[Pasted image 20230620122520.png]]


