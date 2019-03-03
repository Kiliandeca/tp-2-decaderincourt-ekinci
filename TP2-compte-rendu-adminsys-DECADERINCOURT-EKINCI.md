# TP2 BASH 
# Kilian Decaderincourt et Bilge Ekinci
## Groupe 16 - 25/02/2019

### TP 2 - Bash

### Exercice 1 - Variables d'environnement
1. Bash trouve les commandes tapées par l'utilisateur dans les dossiers bin qui sont contenus dans la variable d'environnement path. On y accède en tapant : 
```
echo $PATH
```
Cette commande va afficher trois dossiers.

2. Pour permettre à ```cd``` tapée sans argument de revenir à notre répertoire personnel on utilise la variable d'environnement :
```
$PATH
```

3. La variable ```LANG``` sert à enregistrer la langue que les logiciels vont utiliser pour communiquer avec l'utilisateur.
La variable ```PWD``` enregistre le chemin du dossier courant de l'utilsiateur (current working directory).
La variable ```OLDPWD``` enregistre le chemin précédent le chemin actuel.
La variable ```SHELL``` enregistre le dossier dans lequel on retrouve toutes les commandes du SHELL.
La variable ```_```

4. Pour créer une variable locale on tape : 
```
MY_VAR="bikini" 
```
Pour vérifier que celle ci existe, on va taper (et cela va afficher le contenu de notre variable) :
```
echo $MY_VAR
```

5. En tapant ```bash``` le bash actuel ouvre un nouveau bash. La variable ```MY_VAR``` créée juste avant n'existe donc plus car le nouveau bash ne garde pas en compte les variables locales de l'ancienne session. 
On tape ```exit``` pour revenir à l'environnement initial.

6. Pour exporter la variable ```MY_VAR``` en variable d'environnement, on tape ```export MY_VAR```
On retape ```bash``` et cette fois, en ayant fait un ```echo $MY_VAR``` dans le nouveau bash, on a bien le contenu de notre variable qui s'affiche. Cela est du au fait que la variable est une variable d'environnement qui est globale.

7. On crée la variable d'environnement ```NOMS``` qui a pour contenu nos noms de binômes séparés par un espace.
```
export NOMS='Ekinci Decaderincourt'
```
Pour vérifier que l'affectation est correcte, on tape : 
```
echo $NOMS
```

8. Pour écrire une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” en utilisant la variable NOMS, on tape :
```
COMMANDE="echo Bonjour à vous deux, $NOMS !"
```
Pour utiliser cette commande, on tape : 
```
$COMMANDE
```

9. Si on donne une valeur vide à une variable, cela ne va rien affecter à celle-ci mais elle sera toujours existante, alors qu'avec ```unset``` la variable sera totalement supprimée.

10. On utilise ```echo``` pour écrire exactement ```$HOME=chemin``` ce qui nous donne : 
```
echo '$HOME = '$HOME
```
Cela est interprété comme ```$HOME = /home/biki``` où ```biki``` est notre nom d'utilisateur.

### Programmation Bash

Dans un dossier ```script``` dans notre répertoire personnel dans lequel on enregistre tous nos scripts.
On crée le dossier ```script``` : 
```
cd 
mkdir script
```
On ajoute le chemin vers script à notre PATH : 
```
export PATH=${PATH}:${HOME}/script
```

### Exercice 2 - Contrôle de mot de passe

On crée le fichier ```testpwd.sh``` et on s'attribue tous les droits : 
```
nano testpwd.sh
chmod u+x testpwd.sh
```

On rédige le corps du script ```testpwd.sh``` qui va demander de saisir un mot de passe et vérifier qu'il correspond au contenu de ```$PASSWORD```.
Le mot de passe saisi par l'utilisateur ne s'affiche pas.
```bash
#!/bin/bash

password=bikini

read -p 'Saisissez le mot de passe top secret svp : ' -s input

if [ $input = $password ]; then  
  echo 'Bienvenue Biki'
else 
  echo "Mais vous n'êtes pas Biki !"
fi
```

### Exercice 3 - Expressions rationnelles

Écriture d'un script qui prend un paramètre et utilise la fonction is_number() pour vérifier que ce paramètre
est un nombre réel.

On crée le fichier ```testnumber.sh``` et on s'attribue tous les droits :
```
nano testnumber.sh
chmod u+x testnumber.sh
```

testnumber.sh : 
```bash
#!/bin/bash

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
return 1
else
return 0
fi
}

is_number $1

if [ $? -eq 0 ] ; then
  echo "Le nombre entré en argument est réel"
else
  echo "Le nombre entré en argument is bullshit"
fi
```

### Exercice 4  - Contrôle utilisateur
 
Écriture d'un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le
script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”,
où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre
script, le message doit changer automatiquement)

On crée le fichier ```testuser.sh``` et on s'attribue tous les droits :
```
nano testuser.sh
chmod u+x testuser.sh
```

```bash
#!/bin/bash

if [ $# -ne 1 ] ; then
  echo "Utilisation : ${0##*/} nom_utilisateur"
  exit 1
fi

grep ^$1 /etc/passwd -q
if [ $? -eq 0 ]; then
  echo "L'utilisateur $1 existe !"
else 
  echo "$1 n'existe pas voyons !"
fi
```

### Exercice 5 - Factorielle

Écriture d'un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera que
l’utilisateur saisit toujours un entier naturel).

On crée le fichier ```factorielle.sh``` et on s'attribue tous les droits :
```
nano factorielle.sh
chmod u+x factorielle.sh
```

```bash
#!/bin/bash

result=1

for i in $(seq 1 $1)
do
  result=$((result*i))
done

echo $result
```

### Exercice 6 - Le juste prix

Écriture d'un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner.
Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM).

On crée le fichier ```justeprix.sh``` et on s'attribue tous les droits :
```
nano justeprix.sh
chmod u+x justeprix.sh
```

```bash
#!/bin/bash

aleat=$ ((($RANDOM%1000) +1))

read -p "Tentez de deviner le nombre mystère si vous le pouvez ! :" mystere

if [ $mystere -eq $aleat ] ; then
  echo "Bien joué, vous avez trouvé le nombre mystère du premier coup"
fi

while [ $mystere -ne $aleat ]
do
  if [ $mystere -gt $aleat ] ; then
    echo "C'est moins !"
    read -p "Retentez votre chance, saisissez un nombre :" mystere
  elif [ $mystere -lt $aleat ] ; then
    echo "C'est plus !"
    read -p "Retentez votre chance, saisissez un nombre :" mystere
  else 
    echo "Vous êtes un champion, vous avez trouvé le nombre mystère!"
    exit 0
  fi
done
```

### Exercice 7 - Statistiques

```bash

function is_number()
{
  re='^[+-]?[0-9]+([.][0-9]+)?$'
  if ! [[ $1 =~ $re ]] ; then
    return 1
  else
    return 0
  fi
}

mini=$1;
maxi=$1;
somme=0;
effectif=$#

while [$# -gt 0] ; do

  is_number $1
  
  if [ $? -eq 1] ; then
    exit 1
  fi

  if [ $1 -lt $mini ] ; then
    mini=$1
  fi
  if [ $1 -gt $maxi ] ; then
    maxi=$1
  fi
  somme=$((somme+$1))
  shift
done
echo "minimum: $mini"
echo "maximum: $maxi"
echo "moyenne: $((somme/effectif))"
```
