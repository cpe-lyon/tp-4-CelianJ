# TP 4

## Exercice 1

#### 1

Pour mettre a jour le système, on utilise la commande `sudo apt update`.

#### 2
Afin de faire un alias a la commande `sudo apt update`, on va dans le fichier .bashrc, on ajoute la ligne `alias upd='sudo apt update'`. On utilise ensuite la commande `source ~/.bashrc` pour prendre en compte les modifications apportés au .bashrc et on peut maintenant utiliser la commande `upd`.

#### 3

Lorsque l'on utilise la commande `cat dpkg.log` dans /var/log, on obtient a la fin les 5 derniers paquets installé sur la machine.

#### 4

Afin d'obtenir les derniers paquets installés avec apt, on utilise la commande `apt list -i`.

#### 5

Pour obtenir le nombre de paquets installés sur la vm, on utilise les commandes `apt list -i | wc -l` et `dpkg -l | wc -l`. Dpkg affiche plus de ligne tout simplement car il y a des lignes d'informations.

#### 6

Afin de compter les fichiers disponible sur Ubuntu on utilise la commande `apt list | wc -l`. On obtient le résultat 68744.

#### 7

Pour installer `glances`, `tldr` et `hollywood`, on utilise `sudo apt install`. Ces différents programmes sont des simulations de genres de centres de controle façon matrix.

#### 8

On utilise la commande `apt search sudoku` pour trouver tous les paquets se rapportant a ce mot clé et donc pour la plupart a des paquets permettant de jouer au sudoku.

## Exercice 2

La commande `ls` est installée à partir du paquet `coreutils`

`which -a ls | xargrs dpkg -S | cut -d: -f1`

```bash
#! /bin/bash
echo -n "entrez le nom de la commande : " ;
read;
which -a ${REPLY} | xargrs dpkg -S 2>/dev/null | cut -d: -f1
```

## Exercice 3
```bash
#! /bin/bash

if dpkg -l | grep -q $1 ; then
echo "installé"
else
echo "not installed"
fi
```

## Exercice 4 
_Programmes installés_ : ``basename, cat, chgrp, chmod, chown, chroot, cksum, comm, cp, csplit, cut, date, dd, df, dir, dircolors, dirname, du, echo, env, expand, expr, factor, false, fmt, fold, groups, head, hostid, hostname, id, install, join, kill, link, ln, logname, ls, md5sum, mkdir, mkfifo, mknod, mv, nice, nl, nohup, od, paste, pathchk, pinky, pr, printenv, printf, ptx, pwd, readlink, rm, rmdir, seq, sha1sum, shred, sleep, sort, split, stat, stty, su, sum, sync, tac, tail, tee, test, touch, tr, true, tsort, tty, uname, unexpand, uniq, unlink, uptime, users, vdir, wc, who, whoami et yes`` 
Le programme "[" est un alias pour le programme test. test compare des valeurs et vérifie les types des fichiers. 

## Exercice 5 

`emacs` et `lynx` sont des interfaces graphiques comme `vim` ou `nano`. Ces commandes permettent d'éditer des fichiers de manière plus simple que via `echo` par exemple.

## Exercice 6

Après avoir fait les commandes nécéssaires à l'installation de Java. 

On ouvre le dossier `/etc/apt/sources.list.d`, et voici le contenu du noueavu fichier `linuxupridsing-ubuntu-java-jammy.list` :

<img src="https://media.discordapp.net/attachments/1017478318934724638/1021709278416994394/unknown.png">

Il contient les lien des paquets .deb.

## Exercice 7 - Installation d’un logiciel à partir du code source

On clone le github avec :

`git clone https://gitlab.com/jallbrit/cbonsai` 

Ensuite, on va dans le dossier `cd cbonsai`. Puis, avec `mdless`, on affiche le readme. 

On suit les instructions et on installe les paquets manquants. 

## Exercice 8 - Création de dépôt personnalisé

### Création d’un paquet Debian avec dpkg-deb

On fait l’arborescence demandée : 
```

scripts └───origine-commande │ └───DEBIAN │ │ control │ │ └───usr │ └───local │ └───bin │ │ origine-commande │

```
On build le paquet avec `dpkg-deb --build origine-commande`.

<img
src="https://cdn.discordapp.com/attachments/1017478318934724638/1021716452702695474/unknown.png">

### Création du dépôt personnel avec reprepro

On fait l’arborescence demandée avec `mkdir` puis `nano distributions` : 
```

repo-cpe └───conf │ │ distributions │ └───packages │  

```
On construit le paquet avec la commande `reprepro -b . includedeb origine-commande.deb`.

### Signature du dépôt avec GPG

On générère la clé avec `gpg --gen-key` et dans le fichier de config on ajoute `SignWith: yes`.

On ajoute la clé précédeament créeer dans le déport : `reprepro --ask-passphrase -b . export`.

Et pour finir, on met la clé dans celles connues par APT dans un fichier 'public.key' avec `sudo apt-key add public.key`. 
