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

Le plus simple reste d'installer Veracrypt sur son PC Win perso
et de créer ce qu'il faut sur le HDD pour le mettre en mode "portable".


Tools -> Traveler Disk Setup
Outils -> Paramétrage de disque nomade Veracrypt
Execution sur le HDD vide, creation d'un repertoire Veracrypt
qui contient des binaires desormais



### Installation binaires Linux
https://askubuntu.com/a/847135

l'installation des binaires Linux se fait par simple copie.

$ ls /media/seb/Seagate\ Expansion\ Drive/VeraCrypt/
 Languages/               VeraCryptExpander-x64.exe*   veracrypt.sys*
 VeraCrypt.exe*          'VeraCrypt Format.exe'*       VeraCrypt-x64.exe*
 VeraCryptExpander.exe*  'VeraCrypt Format-x64.exe'*   veracrypt-x64.sys*

$ cd /media/seb/Seagate\ Expansion\ Drive/VeraCrypt/

$ mkdir bin

$ cp -p /usr/bin/veracrypt bin/

$ ll bin
total 4276
drwxrwxrwx 1 seb seb     152 mars   2 21:44 ./
drwxrwxrwx 1 seb seb    4096 mars   2 21:43 ../
-rwxrwxrwx 1 seb seb 4372048 août   7  2020 veracrypt*

$ ./bin/veracrypt 

(veracrypt:410196): Gtk-CRITICAL \*\*: 21:44:22.441: gtk_widget_get_scale_factor: assertion 'GTK_IS_WIDGET (widget)' failed
21:44:28: Debug: window wxMenuBar(0x555ac661a320, ) lost focus even though it didn't have it

=> l'execution se passe OK


---
## Configuration 

### Creation des volumes

https://veracrypt.fr/en/Beginner%27s%20Tutorial.html
Creation du volume "roms" contenant les ROMs et emulateurs
taille : 2 Go

La creation par GUI, le montage par GUI se comporte OK
depuis le bin linux intégré.

### Tests ouvertures/fermetures depuis le HDD

Montage via ligne de commande :
`veracrypt [options] [Volume path] [Mount point]`

veracrypt -t -h | less

$ sudo VeraCrypt/bin/veracrypt -t roms.hc /media/veracrypt1/
[sudo] Mot de passe de seb : 
Enter password for /media/seb/Seagate Expansion Drive/roms.hc: 
Enter PIM for /media/seb/Seagate Expansion Drive/roms.hc: 
Enter keyfile [none]: 
Protect hidden volume (if any)? (y=Yes/n=No) [No]: 
=> cela fonctionne mais il y a trop d'informations à entrer ?


$ sudo VeraCrypt/bin/veracrypt -t -k "" --pim=0 --protect-hidden=no roms.hc /media/veracrypt1/
Enter password for /media/seb/Seagate Expansion Drive/roms.hc: 
=> là ça marche 

Pour unmount :
sudo VeraCrypt/bin/veracrypt -t -d \[volume\]
on peut préciser le volume, sinon ce sont tous les volumes
qui seront démontés

=> Les opérations testées sont OK depuis le pc linux - qui contient
les binaires pour veracrypt.

### Tests depuis le RPi (NAS)
comment se comporte OMV avec le HDD ?





### idées

. créer un script vc dans le répertoire veracrypt, equivalent à
  . trouver le chemin absolu du script, ajouter bin/veracrypt
  . lancer "bin/veracrypt -t" + le reste des args
  . equivalent à veracrypt mais en cli
. créer un script + fichier de config
  . fichier de config qui liste volume (.hc) et dir par défaut
    pour montage (/media/veracryptX)
  . script qui lance les cli pour monter les volumes en matchant
    les dirs   





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
