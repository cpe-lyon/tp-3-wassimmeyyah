## Wassim MEYYAH - 3ICS



# Exercice 1. Variables d'environnement -

### 1 -
```bash
sudo groupadd dev ; sudo  groupadd infra 
```

### 2 - 
```bash
sudo useradd -m alice ; sudo useradd -m bob ; sudo useradd -m charlie ; sudo useradd -m dave
sudo usermod -s /bin/bash alice ; sudo usermod -s /bin/bash bob ; sudo usermod -s /bin/bash charlie ; sudo usermod -s /bin/bash dave
```

### 3 -
```bash
sudo usermod -a -G dev alice
sudo usermod -a -G dev bob
sudo usermod -a -G dev dave
sudo usermod -a -G infra bob
sudo usermod -a -G infra charlie
sudo usermod -a -G infra dave 
```

### 4 - 
```bash
cat /etc/group 
cat /etc/gshadow
```

### 5 - 
```bash 
sudo chgrp dev /home/alice 
sudo chgrp dev /home/bob
sudo chgrp infra /home/charlie
sudo chgrp infra /home/dave
```

### 6 - 
```bash
sudo usermod -g dev alice
sudo usermod -g dev bob
sudo usermod -g infra charlie
sudo usermod -g infra dave
```

### 7 - 
```bash
sudo chmod dev /home/dev
sudo chgrp infra /home/infra

sudo chmod g+w dev
sudo chmod g+w infra
```

### 8 - 
Pour que seul le propriétaire ait le droit de renommer ou de supprimer un fichier, il faudrait y inclure un Sticky Bit. On aurait donc : 
```bash
chmod +t dev ; chmod +t infra
```

### 9 - 
Il est impossible d'ouvrir une session en tant que Alice. Le mot de passe n'étant pas encore paramétré, le compte n'est pas activé.

### 10 -
```bash
sudo passwd alice
su alice
```

### 11 -
La commande id permet d'obtenir le gid et l'uid 
```bash 
id alice
```

### 12 - 
```bash
id -nu 1003
```

### 13 -
```bash
getent group dev
```
Le groupe dev a un id correspondant à 1001

### 14 - 
```bash
getent group GID 1002
```

### 15 - 
Pour supprimer Charlie du groupe Infra, il faut utiliser la commande `sudo gpasswd -d Charlie Infra`. 


### 16 - 
```bash
sudo usermod --expiredate 2023-06-1 dave
sudo chage -m 5 -W 14 -I 30 -M 90 dave
```

17. L'interpréteur de commandes de l'utilisateur root est '#'

18. L'utilisateur nobody sert uniquement à exécuter dess commandes ne demandant que peu de permissions. 

19. Par défaut, la commande sudo garde le mot de passe en mémoire pendant 15 minutes. Si l'on veut que sudo oublie le mot de passe, il faut entrer la commande `sudo -K`


# Exercice 2. Gestion des problèmes - 

### 1  - 
```bash
cd ~
mkdir test 
cd test
cat < fichier
  lignes
  de 
  texte
```
On vérifie ensuite quels sont les droits sur "test" et sur "fichier" : ```cd .. ; ls -l``` : le dossier "test" est en 775 (rwxrwxr-x) tandis que le fichier "fichier" est en 664 (-rw-rw-r--). 

### 2 -
```bash
chmod ugoa-rwx fichier
```
Il nous est désormais impossible d'accéder au contenu du fichier ou de le modifier.
Cependant, en entrant en mode root à l'aide de la commande ```sudo nano fichier``` il est désormais possible de manipuler le fichier à sa guise. On peut en déduire que l'utilisateur root est "au dessus" de ces permissions et qu'il peut influer sur tous les dossiers du système comme bon lui semble.  


### 3 - 
```bash
cd test
chmod u+wx fichier
echo "echo Hello" > fichier
```
Aucun message d'erreur ne s'affiche, le fichier a donc du être correctement modifié. Néanmoins, étant donné que l'on ne dispose pas du droit de lecture, il nous est impossible de le vérfier.

### 4 - 
Il nous est impossible d'éxecuter le fichier : la permission nous est refusé. Cependant, lorsque l'on tente d'exécuter le fichier en mode root avec ```sudo ./fichier```, ce dernier est exécuté.

### 5 - 
```bash
cd test
chmod u-r ~/test
```
Tandis qu'il nous était possible de lister les fichiers du répertoire avant l'exécution de la commande précédente, il nous est désormais impossible de le faire. Il nous est cependant possible de l'exécuter étant donné que nous disposons des droits dessus.

### 6 - 
```bash
touch nouveau
mkdir sstest 
chmod u-w nouveau sstest/
nano nouveau
````

### 7.
Le fait qu'il n'y ait pas de droit d'éxécution empeche de rentrer dans le dossier, mais également d'effectuer une modification des fichiers qu'il contient.

### 8.
On ne peut pas modifier les droits du dossier dans lequel on se trouve.

### 9.
```bash
chmod  g+r fichier
```

### 10.
```bash
umask 007
````
### 11.
```bash
umask 755
````

### 12.
```bash
umask 744
```
### 13. 
- chmod u=rx, g=wx, o=r -> chmod 534
- chmod uo+w,g-rx -> chmod 670
- chmod 653 -> chmod rw-r-x-wx
- chmod u+x,g=w,o-r -> chmod 520

### 14. 
```bash
-rw-r--r--   [...] passwd
```
Personne n'a les droits

