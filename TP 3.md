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
id 1003
```

### 13 -
```bash
cat /etc/group
```
Le groupe dev a un id correspondant à 1001

### 14 - 

