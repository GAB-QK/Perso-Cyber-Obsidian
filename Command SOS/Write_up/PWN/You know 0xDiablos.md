---
id: You
created_date: 19/06/2023
updated_date: 19/06/2023
type: note
---

#  0xDiablos
- **🏷️Tags** :  #06-2023 #buffer #overflow #stack #GDB #reverse #PWN 

### Observation 
1 - Première étape du challenge on étudie le type de fichier fournie

![[Pasted image 20230616162442.png]]

- on a donc un binaire que l'on peut executer donc executons le :
![[Pasted image 20230616162542.png]]

>[!info]
>on a donc un input a entrer et l'output est le même que l'input.

- On peut donc essayer de dé compiler le binaire avec l'outil **Ghidra** pour mieux comprendre son fonctionnement :

![[Pasted image 20230616162727.png]]

- on peut observer la présence de plusieurs fonctions, en étudiant la fonction **"main"** nous pouvons observer le comportement suivant :

![[Pasted image 20230616162818.png]]

- on a donc l'output qu'on a pue observer ultérieurement sur l'execution du binaire suivis de l'appel de la fonction **"vuln()"** suivante :

![[Pasted image 20230616162947.png]]

On peut retrouver le comportement du binaire dans cette fonction, de plus on peut remarquer la taille attribué à la variable **"local_bc"** qui est de **180**.

### Test et exploit

- on peut donc essayer sur l'executable une petite tentative de segmentation fault.
- 
![[Pasted image 20230616163327.png]]

>[!info]
>on observe donc bien un segfault il ya donc surement un bufferflow à exploiter. Il nous faut donc découvrir comment et ou exploiter le l'over flow.


>pour cela nous allons utiliser GDB :


![[Pasted image 20230616163509.png]]

>[!tip]
>précision : il faut préalablement installer **peda** à GDB ( facile d'installation voir internet )

> En utilisant la commande "start" on obtient le résultat suivant : 

![[Pasted image 20230616163644.png]]

- En retournant sur ghidra on peut étudier les fonctions présente dans le binaire, on peut effectivement remarquer qu'une des fonctions se prénomme **"flgag()"**, elle prend deux paramètres.

![[Pasted image 20230619110946.png]]

>[!Objectif]
>nous voulons donc trouver l'adresse de la fonction **flag()**, et l'appeler en utilisant le buffer overflow.

>retournons dans GDB et créons un pattern random de 200 char pour crée l'overflow.

![[Pasted image 20230619111927.png]]

>[!Objectif]
>maintenant nous souhaitons lancer le programme avec le pattern que nous venons de crée, pour cela nous utilisons la commande suivante:

![[Pasted image 20230619112105.png]]

>[!Note]
>note ( "r" pour "run")

- On obtient donc le résultat suivant :

![[Pasted image 20230619112208.png]]

>[!Observation]
>on remarque donc qu'il y a un bien un overflow sur la stack et cela nous l'est indiqué par :

![[Pasted image 20230619112503.png]]


>[!Objectif]
>nous cherchons donc maintenant les **"offset"** nous permettant de bien localiser  a quel spot on peut commencer a écrire notre payload.
>pour cela on utilise la commande suivante avec l'adresse de l'EIP 

![[Pasted image 20230619114357.png]]

> Pour récupérer l'adresse de la fonction et voir ou elle commence dans le binaire, on utilise la commande suivante :

![[Pasted image 20230619122400.png]]

on récupère la première adresses indiquer dans l'output.

>[!Objectif]
>Avec toutes ces informations de récuperer on souhaite maintenant crée notre payloads.

``` bash
python3 -c "import sys; sys.stdout.buffer.write(b'A'*188+b'\xe2\x91\x04\x08'+b'\xef\xbe\xad\xde\x0d\xd0\xde\xc0')" > payload.txt

```

>on écrit donc 188 fois la lettre 'A' on ajoute en plus avec +b'...' l'adresse de la fonction suivis de +b'...' avec les deux paramètres que la fonction demande.
>on récupère l'adresse des paramètre de la manière suivante.

![[Pasted image 20230619122958.png]]

### Exploit sur le binaire

On a donc les deux adresses suivantes a indiquer dans notre payload 
**"EF BE AD DE"** et **"0D D0 DE C0"**
après cela on crée le payload ce qui nous donne :

![[Pasted image 20230619123345.png]]

>[!Résultat]
>on teste donc notre binaire de la manière suivante ;

![[Pasted image 20230619123412.png]]


>[!Success]
>on a donc une réponse positive il ne nous reste plus qu'a l'essayer coté serveur.

![[Pasted image 20230619123652.png]]


>[!Warning]
>cela prend un peu de temps mais l'output du serveur sera le flag.