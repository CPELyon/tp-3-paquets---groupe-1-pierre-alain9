# Exercice 1. Commandes de base

1. Pour mettre à jour le système :

```sudo apt update && sudo apt upgrade```

update met à jour la liste des paquets qui peuvent être mis à jour et upgrade fais les mises à jour.

2. Afin de faire des mises à jour plus facilement, on peut créer un alias des deux commandes de la question 1 :

```alias maj="sudo apt update && sudo apt upgrade"```

Si on veut garder cet alias même après un redémarrage du système, il faut l'écrire dans **.bashrc** (fichier de configuration de bash qui s'exécute au démarrage), qui se situe dans le dossier personnel, après la ligne "*some more ls aliases*".

3. On veut connaitre les 5 derniers paquets installés sur la machine :

```grep 'installed' /var/log/dpkg.log | tail -5 | cut -d' ' -f5 | cut -d: -f1```

L'espace avant *installed* permet d'éviter les package *half-installed*.

4.

```grep "apt install" /var/log/apt/history.log | cut -d' ' -f4```

  

5. Pour savoir le nombre total de paquets installés sur la machine :

```dpkg -l | grep '^ii' | wc -l``` ou ```apt list --installed | wc -l```

"^ii" de la première commande signifie que l'on cherche "ii" au début des lignes. Si on enlève le pipe | et la commande wc, on a les informations sur les paquets installés.

Avec la première commande, on obtient 571 alors qu'avec la deuxième, on a 572. La ligne supplémentaire vient de la première ligne de la deuxième commande qui n'est pas un paquet (c'est "listing...").

On obtient un nombre de lignes différent de celui obtenu lors de la question 3 car le fichier dpkg.log est limité en nombre de lignes.

6. Pour savoir le nombre de paquets disponibles en téléchargement sur les dépôts d'Ubuntu, on fait :

```apt list | wc -l```

On obtient 62571 paquets disponibles.

7. Pour avoir des informations sur un paquet, on fait :

```apt show nomPackage```

**Glances** est un outil de surveillance du système fondé sur la bibliothèque Curses.

**tldr** permet d'obtenir des informations condensées sur une commandes.

**Hollywood** reproduits des interfaces qu'on peut voir dans les films d'Hollywood.

Pour installer un paquet :

```apt install nomPackage```

8. Pour rechercher un paquet qui effectue une action que l'on veut, on fait:

```apt search action```


# Exercice 2

Commande pour récupérer le nom du paquet d'installation de la commande ls
```
which -a ls | xargs dpkg -S | cut -d: -f1 ou dpkg -S $(which -a ls) | cut -d: -f1
```
On peut alors écrire un script appelé ''origine_commande.sh'' permettant de pouvoir connaitre la paquet de chaque commande.
Pour cela je crée un script ``` vim origine_commande.sh``` qui contient ces commandes 
```
#!/bin/bash
which -a $1|xargs dpkg -S | cut -d: -f1
```
On fait appel à notre programme en mettant en argument la commande à chercher
```
./origine_commande.sh ls
```

# Exercice 3
Connaitre le statut d'un package
``` 
dpkg -l apt | grep '^ii' && echo "Installé" || echo "Non Installé"
```

# Exercice 4
Pour lister il faut ``` dpkg -L coreutils```
On obtient alors la liste de tous les programmes du package coreutils. On perçoit un programme s 'appelant [. Celui-ci est ici car il permet de remplacé le programme test qui crée des expressions conditionnelles
je sais pas j'ai pas trouver pour l'instant!!

# Exercice 5
Installation de aptitude
``` sudo apt install aptitude```
pour lancer aptitude il suffit d'écrire
```aptitude```
Une fois dans la partie graphique afin de rechercher un programme il faut réaliser un /lenomduprogramme et parcourir la liste de recherche en appuyant sur n .
Une fois le bon programme trouvé, il suffit de l'installer en appuyant deux fois sur g . La commande u permet de update les packages et U pour mettre à jour .
emacs est un éditeur de texte alors que lynx est un navigateur web mais uniquement utilisant ddes lignes de commande.

# Exercice 6

Nous avons des logicielles qui ne figurent pas dans les dépots officielles et il faut donc utiliser le ppa afin de l'installer. Nous allons ici prendre l'exemple de java qui est actuellement développer par oracle
``` 
sudo add-apt-repository ppa:linuxuprising/java 
sudo apt update 
sudo apt install oracle-java15-installer
```
Dans le fichier qui a été créé dans le répertoire /etc/apt/sources.list.d, on remarque quand lisant ce fichier on retrouve l'url permettant l'installation de java sur ma machine (la source du ppa) (http://ppa.launchpad.net/linuxuprising/java/ubuntu focal main)

# Exercice 7
Clone le gitlab qu'on doit installer en local .
```
git clone https://gitlab.com/jallbrit/cbonsai
```
On nous a demandé d'installer ncurses 
```
sudo apt install libncursesw5-dev libncurses5-dev

sudo apt install gcc pkg-package  (rajoute des packages qui ne sont pas installer la premiere fois et qui sont utiles)
```
```
cd cbonsai/
```
Après avoir installer make, réaliser l'installation en local
```
make install PREFIX=~/.local
```
On veut maintenant l'installer de facon à obtenir un paquet. On obtien alors un cbonsai.deb ce qui est très interessant dans l'utilisation.
```
sudo apt install checkinstall

sudo checkinstall
```


