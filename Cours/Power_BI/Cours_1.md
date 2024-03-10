---
id: Cours_1
created_date: 18/12/2023
updated_date: 18/12/2023
type: note
---

#  Cours_1
- **🏷️Tags** :  #12-2023 #buisness_intelligence #SQL #courses #introduction

## 📝 Notes

### Processus et schématisation 
## 1. **Tables de Base (Source Transactional Area - STA)**
- Ces tables représentent les données brutes provenant de différentes sources transactionnelles.
- Exemples : Tables de ventes, de clients, de produits, etc.
- Relations : Les tables de base sont connectées aux ODS pour le transfert de données.
## 2. **Operational Data Store (ODS)**
- L'ODS sert de zone intermédiaire pour le nettoyage et la consolidation des données.
- Relations :
    - En entrée, reçoit des données des STA.
    - En sortie, alimente la Data Warehouse.
## 3. **Data Warehouse (DWH)**
- Cœur de l'architecture BI, où les données sont stockées pour des analyses approfondies.
- Utilise la modélisation en étoile.
- Comprend une table de faits et plusieurs tables de dimensions.
    - **Table de faits** : Stocke les mesures quantitatives et les indicateurs clés.
    - **Tables de dimensions** : Contiennent des attributs descriptifs relatifs aux mesures dans la table de faits.
## 4. **Modélisation en Étoile**
- Au centre se trouve la table de faits, entourée par des tables de dimensions.
- Chaque table de dimension est liée à la table de faits par une clé étrangère.
- Exemple de tables de dimensions : Clients, Produits, Temps, Régions.


Les systèmes OLTP (Online Transaction Processing) et OLAP (Online Analytical Processing) sont deux types de systèmes de gestion de bases de données qui servent des objectifs différents dans le monde des affaires et de l'informatique.

### OLTP (Online Transaction Processing)

#### À Quoi Ça Correspond
- **Utilisation**: Gère les transactions quotidiennes d'une entreprise.
- **Exemples**: Systèmes de point de vente, systèmes de réservation, systèmes bancaires.
- **Structure de Données**: Optimisée pour les transactions rapides et efficaces.
- **Nature des Opérations**: Insertions, mises à jour, et suppressions fréquentes.

#### Avantages
- **Rapidité**: Conçu pour des temps de réponse rapides et la gestion de multiples transactions simultanées.
- **Fiabilité**: Haut niveau de fiabilité et de disponibilité.

#### Inconvénients
- **Non optimisé pour l'analyse**: Difficulté à effectuer des analyses complexes sur les données.
- **Volume de données**: Gère moins bien de grands volumes de données historiques.

### OLAP (Online Analytical Processing)

#### À Quoi Ça Correspond
- **Utilisation**: Conçu pour l'analyse de données complexes et l'aide à la prise de décision.
- **Exemples**: Systèmes de reporting et d'analyse, data warehouses.
- **Structure de Données**: Souvent organisée en cubes OLAP ou en modélisation en étoile/ flocon de neige.
- **Nature des Opérations**: Requêtes de lecture principalement, avec des agrégations complexes et des analyses multidimensionnelles.

#### Avantages
- **Analyse Multidimensionnelle**: Permet des analyses complexes sur de multiples dimensions.
- **Gestion des Grands Volumes**: Efficace pour travailler avec de grands ensembles de données historiques.

#### Inconvénients
- **Complexité**: Plus complexe à mettre en place et à maintenir.
- **Coût**: Peut être plus coûteux en termes de stockage et de traitement causé par la redondance, en raison de la taille et de la complexité des données.

En résumé, les systèmes OLTP sont essentiels pour la gestion quotidienne des transactions d'une entreprise, tandis que les systèmes OLAP sont utilisés pour des analyses complexes et la prise de décision stratégique. Les choix entre OLTP et OLAP dépendent des besoins spécifiques de l'entreprise en matière de traitement et d'analyse de données.


## Questions/Thoughts


## 🔗 Links
- 