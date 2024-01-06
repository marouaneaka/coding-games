# Pertes En Bourse

## Description du Puzzle

Une entreprise spécialisée dans la finance réalise une étude sur les pires investissements en bourse et souhaite développer un programme à cet effet. Ce programme doit être capable d'analyser une série chronologique de valeurs d'actions pour afficher la plus grande perte qu'il est possible de réaliser en achetant une action à un instant t0 et en la revendant à une date ultérieure t1. La perte est exprimée par la différence de valeur entre t0 et t1. Si aucune perte n'est possible, la perte sera alors égale à 0.

## Entrées du Jeu

**Entrée :**

- Ligne 1 : le nombre n de valeurs en bourse disponibles.
- Ligne 2 : les valeurs ordonnées depuis l'introduction en bourse v1 jusqu'à la dernière valeur connue vn. Les valeurs sont des entiers.

**Sortie :**

La perte maximale p, exprimée négativement s'il y a une perte, sinon 0.

## Contraintes

- 0 < n < 100000
- 0 < v < 231
## Explications
Les boucles for et while calculent toutes les pertes possibles en parcourant la liste des valeurs d'actions. Les pertes sont stockées dans la liste loss.
## Le Code Python

```python
import sys
import math

# Le code auto-généré ci-dessous vise à vous aider à analyser
# l'entrée standard selon l'énoncé du problème.

n = int(input())
valeurs = list()
for i in input().split():
    v = int(i)
    loss = v
    valeurs.append(v)
loss = list()
k=0
for v in valeurs :
    i = 1+k
    while(i< n ):
        loss.append(valeurs[i] - v)
        i +=1
    k+=1  
if min(loss) > 0 :
    print("0")
else:
    print(min(loss))
