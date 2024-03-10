---
id: Minage
created_date: 23/10/2023
updated_date: 23/10/2023
type: note
---

#  Minage
- **🏷️Tags** :  #10-2023 

## 📝 Notes

Le minage de cryptomonnaie sur Windows sans interface graphique (GUI) nécessite plusieurs étapes. Voici un guide simplifié :

**1. Choisissez une cryptomonnaie à miner :**
   - Choisissez une cryptomonnaie compatible avec le minage sur Windows. Des exemples populaires incluent Bitcoin, Ethereum, Litecoin, etc.

**2. Choisissez un logiciel de minage :**
   - Pour Windows, vous pouvez utiliser des logiciels tels que CGMiner, BFGMiner, ou EasyMiner. Chaque cryptomonnaie peut avoir des logiciels spécifiques recommandés, assurez-vous de faire vos recherches en fonction de la monnaie que vous choisissez.

**3. Installez les prérequis :**
   - Vous aurez besoin de certains composants, tels que des pilotes de carte graphique (pour le minage GPU) ou des pilotes de matériel spécifique (pour le minage ASIC). Assurez-vous d'avoir ces éléments à jour.

**4. Configurez votre pool de minage :**
   - Inscrivez-vous sur un pool de minage. Les pools sont des groupes de mineurs qui combinent leur puissance de calcul pour augmenter les chances de trouver un bloc. Choisissez un pool compatible avec la cryptomonnaie que vous minez.

**5. Obtenez une adresse de portefeuille :**
   - Vous aurez besoin d'une adresse de portefeuille pour recevoir les récompenses de minage. Téléchargez et configurez un portefeuille pour la cryptomonnaie que vous minez.

**6. Configurez le logiciel de minage :**
   - Créez un fichier de configuration avec les détails de votre pool, votre adresse de portefeuille et les paramètres spécifiques à la cryptomonnaie que vous minez. Vous devrez également spécifier les informations de votre matériel (par exemple, les cartes graphiques) dans ce fichier de configuration.

**7. Exécutez le script de minage :**
   - Créez un script qui démarre le logiciel de minage avec les paramètres appropriés. Vous pouvez utiliser un fichier de commandes (".bat" pour Windows) pour cela.

**8. Surveillez et optimisez :**
   - Laissez le script s'exécuter et surveillez les performances de votre matériel. Vous pouvez ajuster les paramètres pour optimiser le rendement du minage.

N'oubliez pas de prendre en compte les coûts énergétiques et la rentabilité potentielle avant de vous lancer dans le minage. Assurez-vous également de respecter les lois et réglementations locales concernant le minage de cryptomonnaie.

## scripting exemple 

```batch
@echo off
setx GPU_FORCE_64BIT_PTR 0
setx GPU_MAX_HEAP_SIZE 100
setx GPU_USE_SYNC_OBJECTS 1
setx GPU_MAX_ALLOC_PERCENT 100
setx GPU_SINGLE_ALLOC_PERCENT 100

cgminer --scrypt -o stratum+tcp://nomdupool.com:port -u VotreAdressePortefeuille -p x --gpu-platform 0 -d 0 -I 18 -w 256 --thread-concurrency 8192
```

**Explication :**
- `@echo off` : Désactive l'affichage de chaque commande dans la console.
- `setx` : Configure des variables d'environnement pour optimiser les performances de la carte graphique.
- `cgminer` : C'est la commande pour exécuter CGMiner.
- `--scrypt` : Spécifie l'algorithme de hachage utilisé pour miner Ethereum.
- `-o stratum+tcp://nomdupool.com:port` : Remplacez "nomdupool.com" et "port" par les détails de votre pool de minage.
- `-u VotreAdressePortefeuille` : Remplacez "VotreAdressePortefeuille" par votre propre adresse de portefeuille Ethereum.
- `-p x` : Spécifiez le mot de passe du pool (ici, il est laissé vide).
- `--gpu-platform 0 -d 0` : Indique le numéro de la plateforme GPU et de la carte graphique à utiliser.
- `-I 18` : Configure l'intensité du minage. Vous pouvez ajuster cette valeur en fonction de la performance de votre matériel.
- `-w 256` : Spécifie la largeur du worksize.
- `--thread-concurrency 8192` : Configure la concurrence des threads.

N'oubliez pas de remplacer les éléments en majuscules par vos propres informations. Assurez-vous également que CGMiner et les pilotes de votre carte graphique sont installés correctement.

Sauvegardez ce script avec une extension ".bat" (par exemple, "minage_ethereum.bat") et exécutez-le pour démarrer le processus de minage. Assurez-vous d'adapter les paramètres en fonction de votre matériel et de votre pool de minage.


## Automatisation du script 
### méthode 1:

Pour exécuter automatiquement le processus de minage à l'ouverture ou à l'allumage de votre ordinateur personnel sous Windows, vous pouvez suivre ces étapes :

**1. Créer un raccourci du script :**
   - Faites un clic droit sur votre script de minage (par exemple, "minage_ethereum.bat").
   - Sélectionnez "Créer un raccourci".

**2. Copier le raccourci dans le dossier de démarrage :**
   - Appuyez sur la touche Windows + R pour ouvrir la boîte de dialogue "Exécuter".
   - Tapez "shell:startup" et appuyez sur Entrée. Cela ouvrira le dossier de démarrage de l'utilisateur.

**3. Placer le raccourci dans le dossier :**
   - Copiez le raccourci que vous avez créé à l'étape 1 et collez-le dans le dossier qui vient de s'ouvrir.

Désormais, chaque fois que vous démarrez ou ouvrez votre ordinateur, le script de minage sera exécuté automatiquement.



## Questions/Thoughts


## 🔗 Links
- 