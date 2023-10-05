---
id: GDB
created_date: 05/10/2023
updated_date: 05/10/2023
type: note
---

#  GDB
- **🏷️Tags** :  #10-2023 

## 📝 Notes

### Introduction a GDB

GDB, ou le Débogueur GNU, est le débogueur standard des systèmes Linux développé par le Projet GNU. Il a été porté sur de nombreux systèmes et prend en charge les langages de programmation C, C++, Objective-C, FORTRAN, Java, et bien d'autres.

GDB nous offre des fonctionnalités habituelles de traçabilité telles que les points d'arrêt ou la sortie de la pile d'appels, et nous permet d'intervenir dans l'exécution des programmes. Il nous permet également, par exemple, de manipuler les variables de l'application ou d'appeler des fonctions indépendamment de l'exécution normale du programme.

### AT&T Syntax et Intel Syntax


```bash
htb-student@nixbof32:~$ gdb bow

(gdb) disassemble main
Dump of assembler code for function main:
   0x00000582 <+0>:	lea    0x4(%esp),%ecx
   0x00000586 <+4>:	and    $0xfffffff0,%esp
   0x00000589 <+7>:	pushl  -0x4(%ecx)
   0x0000058c <+10>:	push   %ebp
   0x0000058d <+11>:	mov    %esp,%ebp
   0x0000058f <+13>:	push   %ebx
   0x00000590 <+14>:	push   %ecx
   0x00000591 <+15>:	call   0x450 <__x86.get_pc_thunk.bx>
   0x00000596 <+20>:	add    $0x1a3e,%ebx
   0x0000059c <+26>:	mov    %ecx,%eax
   0x0000059e <+28>:	mov    0x4(%eax),%eax
   0x000005a1 <+31>:	add    $0x4,%eax
   0x000005a4 <+34>:	mov    (%eax),%eax
   0x000005a6 <+36>:	sub    $0xc,%esp
   0x000005a9 <+39>:	push   %eax
   0x000005aa <+40>:	call   0x54d <bowfunc>
   0x000005af <+45>:	add    $0x10,%esp
   0x000005b2 <+48>:	sub    $0xc,%esp
   0x000005b5 <+51>:	lea    -0x1974(%ebx),%eax
   0x000005bb <+57>:	push   %eax
   0x000005bc <+58>:	call   0x3e0 <puts@plt>
   0x000005c1 <+63>:	add    $0x10,%esp
   0x000005c4 <+66>:	mov    $0x1,%eax
   0x000005c9 <+71>:	lea    -0x8(%ebp),%esp
   0x000005cc <+74>:	pop    %ecx
   0x000005cd <+75>:	pop    %ebx
   0x000005ce <+76>:	pop    %ebp
   0x000005cf <+77>:	lea    -0x4(%ecx),%esp
   0x000005d2 <+80>:	ret    
End of assembler dump.
(gdb)

```

### Registre du CPU

#### Registres de données

|**32-bit Register**|**64-bit Register**|**Description**|
|---|---|---|
|`EAX`|`RAX`|Accumulateur est utilisé dans les entrées / sorties et pour les opérations arithmétiques|
|`EBX`|`RBX`|La base est utilisée dans l'adressage indexé|
|`ECX`|`RCX`|Counter est utilisé pour faire pivoter les instructions et compter les boucles|
|`EDX`|`RDX`|Les données sont utilisées pour les E / S et dans les opérations arithmétiques pour les opérations de multiplication et de division impliquant de grandes valeurs large values|


#### Registre de pointeurs

|**32-bit Register**|**64-bit Register**|**Description**|
|---|---|---|
|`EIP`|`RIP`|Le pointeur d'instructions stocke l'adresse décalée de la prochaine instruction à exécuter|
|`ESP`|`RSP`|Le pointeur de pile pointe vers le haut de la pile|
|`EBP`|`RBP`|Le pointeur de base est également connu sous le nom de pointeur de base de pile ou pointeur de cadre qui pointe vers la base de la pile|


À mesure que la Pile (stack) se développe, elle est logiquement divisée en régions appelées Stack Frames, qui allouent la mémoire requise dans la pile pour la fonction correspondante. Un cadre de pile définit un cadre de données avec le début (**EBP**) et la fin (**ESP**) qui est poussé sur la pile quand une fonction est appelée.

Comme la mémoire de la pile est construite sur une structure de données Last-In-First-Out (LIFO), la première étape consiste à stocker la position EBP précédente sur la pile, qui peut être restaurée une fois la fonction terminée. Si nous regardons maintenant la fonction bowfunc, elle ressemble à ceci dans GDB 


```bash
(gdb) disas bowfunc 

Dump of assembler code for function bowfunc:
   0x0000054d <+0>:	    push   ebp       # <---- 1. Stores previous EBP
   0x0000054e <+1>:	    mov    ebp,esp
   0x00000550 <+3>:	    push   ebx
   0x00000551 <+4>:	    sub    esp,0x404
   <...SNIP...>
   0x00000580 <+51>:	leave  
   0x00000581 <+52>:	ret    
```

Le `EBP` dans le cadre de pile est défini en premier lorsqu’une fonction est appelée et contient le `EBP` du cadre de pile précédent. Ensuite, la valeur de `l’ESP` est copiée dans `l’EBP`, créant une nouvelle trame de pile.

```bash
(gdb) disas bowfunc 

Dump of assembler code for function bowfunc:
   0x0000054d <+0>:	    push   ebp       # <---- 1. Stores previous EBP
   0x0000054e <+1>:	    mov    ebp,esp   # <---- 2. Creates new Stack Frame
   0x00000550 <+3>:	    push   ebx
   0x00000551 <+4>:	    sub    esp,0x404 
   <...SNIP...>
   0x00000580 <+51>:	leave  
   0x00000581 <+52>:	ret    
```

Ensuite, un peu d’espace est créé dans la pile, déplaçant `l’ESP` vers le haut pour les opérations et les variables nécessaires et traitées.

#### Prologue

```bash
(gdb) disas bowfunc 

Dump of assembler code for function bowfunc:
   0x0000054d <+0>:	    push   ebp       # <---- 1. Stores previous EBP
   0x0000054e <+1>:	    mov    ebp,esp   # <---- 2. Creates new Stack Frame
   0x00000550 <+3>:	    push   ebx
   0x00000551 <+4>:	    sub    esp,0x404 # <---- 3. Moves ESP to the top
   <...SNIP...>
   0x00000580 <+51>:	leave  
   0x00000581 <+52>:	ret    
```

Ces 3 instructions représente le `Prologue`.

>[!Note] En résumé :
> #### Prologue
>- Le prologue prépare l'environnement nécessaire pour l'exécution de la fonction.
>- Il sauvegarde les valeurs de certains registres (comme EBP, EBX, ESI, EDI) sur la pile (stack).
>- Il alloue de l'espace pour les variables locales de la fonction.
>
>#### Epilogue
> - L'épilogue "nettoie" après l'exécution de la fonction.
> - Il restaure les valeurs des registres qui ont été sauvegardées dans le prologue.
> - Il libère l'espace alloué pour les variables locales en déplaçant le pointeur de pile.

#### Index registers

|**Register 32-bit**|**Register 64-bit**|**Description**|
|---|---|---|
|`ESI`|`RSI`|Source Index est utilisé comme un pointeur d’une source pour les opérations de chaîne|
|`EDI`|`RDI`|Destination est utilisé comme un pointeur vers une destination pour les opérations de chaîne|

#### Compilation au foramt 64-bit 

Un autre point important concernant la représentation de l’assembleur est la dénomination des registres. Cela dépend du format dans lequel le binaire a été compilé. Nous avons utilisé GCC pour compiler le bow. c code en format 32 bits. Maintenant, compilons le même code dans un format 64 bits.

```bash
student@nix-bow:~$ gdb -q bow64

Reading symbols from bow64...(no debugging symbols found)...done.
(gdb) disas main

Dump of assembler code for function main:
   0x00000000000006bc <+0>: 	push   rbp
   0x00000000000006bd <+1>: 	mov    rbp,rsp
   0x00000000000006c0 <+4>: 	sub    rsp,0x10
   0x00000000000006c4 <+8>:  	mov    DWORD PTR [rbp-0x4],edi
   0x00000000000006c7 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x00000000000006cb <+15>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000000006cf <+19>:	add    rax,0x8
   0x00000000000006d3 <+23>:	mov    rax,QWORD PTR [rax]
   0x00000000000006d6 <+26>:	mov    rdi,rax
   0x00000000000006d9 <+29>:	call   0x68a <bowfunc>
   0x00000000000006de <+34>:	lea    rdi,[rip+0x9f]
   0x00000000000006e5 <+41>:	call   0x560 <puts@plt>
   0x00000000000006ea <+46>:	mov    eax,0x1
   0x00000000000006ef <+51>:	leave  
   0x00000000000006f0 <+52>:	ret    
End of assembler dump.
```

Cependant, nous examinerons d’abord la version 32 bits du binaire vulnérable. L’instruction la plus importante pour nous à l’heure actuelle est l’instruction `call`. L’instruction `call` est utilisée pour appeler une fonction et effectue deux opérations :

1. il pousse l’adresse de retour sur la pile de sorte que l’exécution du programme puisse être poursuivie après que la fonction ait atteint son objectif,
2. il remplace ` (EIP)` `par la destination` de l’appel et commence l’exécution.

## Questions/Thoughts


## 🔗 Links
- 