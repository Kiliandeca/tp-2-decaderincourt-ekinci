# TP2 BASH 
# Kilian Decaderincourt et Bilge Ekinci
## Groupe 16 - 25/02/2019

### TP 2 - Bash

### Exercice 1 - Variables d'environnement
1. Bash trouve les commandes tapées par l'utilisateur dans les dossiers bin qui sont contenus dans la variable d'environnement path. On y accède en tapant : 
'''
echo $PATH
'''
Cette commande va afficher trois dossiers.

2. Pour permettre à cd tapée sans argument de revenir à notre répertoire personnel on utilise la variable d'environnement :
'''
$PATH
'''

3. La variable '''LANG''' sert à enregistrer la langue que les logiciels vont utiliser pour communiquer avec l'utilisateur.
La variable '''PWD''' enregistre le chemin du dossier courant de l'utilsiateur (current working directory).
La variable '''OLDPWD''' enregistre le chemin précédent le chemin actuel.
La variable '''SHELL''' enregistre le dossier dans lequel on retrouve toutes les commandes du SHELL.
La variable '''_''' 

4. Pour créer une variable locale on tape : 
'''
MY_VAR="bikini" 
'''
Pour vérifier que celle ci existe, on va taper (et cela va afficher le contenu de notre variable) :
'''
echo $MY_VAR
'''

5. En tapant '''bash''' le bash actuel ouvre un nouveau bash. La variable '''MY_VAR''' créée juste avant n'existe donc plus car le nouveau bash ne garde pas en compte les variables locales de l'ancienne session. 
On tape '''exit''' pour revenir à l'environnement initial.

6. Pour exporter la variable '''MY_VAR''' en variable d'environnement, on tape '''export MY_VAR'''
On retape '''bash''' et cette fois, en ayant fait un '''echo $MY_VAR''' dans le nouveau bash, on a bien le contenu de notre variable qui s'affiche. Cela est du au fait que la variable est une variable d'environnement qui est globale.

7. On crée la variable d'environnement '''NOMS''' qui a pour contenu nos noms de binômes séparés par un espace.
'''
export NOMS='Ekinci Decaderincourt'
'''
Pour vérifier que l'affectation est correcte, on tape : 
'''
echo $NOMS
'''





