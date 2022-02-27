# Veracrypt

- Contexte 
- Plan initial
- Installation 
- Configuration 
- Opération initiale 
- Automatisation
- Conclusion


---
## Contexte

Je veux installer Veracrypt sur un Disque Dur Externe ( appelé HDD )
afin de réaliser une sauvegarde externe de mon NAS (rudimentaire).
Ainsi mes données seront protégées et je pourrais externaliser le disque
( conformément à une strategie backup 3-2-1 [^1] ).

Cahier des charges spécifique :
- pouvoir plugger HDD sur Windows ou Linux et 
  pouvoir récupérer les données avec un mdp
- pouvoir plugger HDD sur NAS et effectuer une copie auto
  NAS --> HDD des données manquantes

Par la suite on pourra effectuer les mêmes opération sur un second HDD
afin de pouvoir faire une rotation.

---
## Plan initial

Afin de se conformer au CdC il faut installer HDD en mode portable.
On aura tous les éxécutables présents sur le HDD.

Les données seront hébergées sur différents "volumes"



  
---
## Installation

Les informations nécessaires pour réaliser l'installation sont disponibles
sur le [site de Veracrypt](https://veracrypt.fr/en/Documentation.html).

### Installation binaires Windows
https://veracrypt.fr/en/Portable%20Mode.html

### Installation binaires Linux
https://askubuntu.com/a/847135


---
## Configuration 

### Creation des volumes


---
## Opération initiale

### Ouverture de volumes, copie de données


---
## Automatisation

### Montage auto du HDD sur le NAS

### Copie auto du NAS vers le HDD


---
## Conclusion









[^1]: [Backup 3-2-1 par Jeff Geerling](https://www.youtube.com/watch?v=S0KZ5iXTkzg)
