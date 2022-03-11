# gcloud



---
## Init

Se faire un compte google cloud platform (gcp)
recherche + "essai gratuit", en haut à droite de la page trouvée.



---
## compute instances = VM

Sélectionner "Compute Engine", dans le menu à droite

On peut créer une VM en choisissant "Instance de VM" à droite,
puis créer. On choisit ses paramètres > E2-micro pour la VM 'gratuite'.
On la lance puis cliquer sur le bouton SSH pour s'y connecter.

Pour + de pratique, on peut installer l'[interface CLI gcloud](https://cloud.google.com/sdk/docs/install)

J'utilise ces alias :
```
alias gci='gcloud compute instances'
alias gssh='gcloud compute ssh'
```

J'ai également créer des "modeles d'instances" (template)
un en CentOS 7 et un en Ubuntu 20.04 avec le "traffic" http,https ouvert

On peut ensuite créer une nouvelle instance à partir d'un modèle et 
s'y connecter :
```
gci create centos-2 --source-instance-template=template-centos7
gssh centos-2
```

Pour arreter la VM :
`gci stop centos-2`

A partir du modele 'web' (le traffic http et https est coché
directement dans le modele), je lance :

```
gci create ub-webtest-1 --source-instance-template="ub2004-web"
gssh ub-webtest-1
```

Une fois connecté un simple
`sudo python3 -m http.server 80`
permet de servir un fichier 'it works'

La creation de la machine nous réponds avec une IP externe.

Debug de la connexion :

```
nmap -Pn -p80 34.105.123.xx
```
nmap me renvoit que le port http est filtered.
Toutes les cases http https sont cochées.

Apparement il faut vérifier les regles de pare-feu !
```
gcloud compute firewall-rules list
# dans mon cas il manque une regle pour le port 80 
gcloud compute firewall-rules create default-allow-http80 --direction ingress --action allow --source-ranges 0.0.0.0/0 --rules tcp:80
```
et ça marche par navigateur !!

