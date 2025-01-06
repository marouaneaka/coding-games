# La Descente

Le jeu consiste en une descente de montagnes virtuelles, où à chaque tour, vous recevez en entrée les hauteurs des montagnes et devez choisir laquelle attaquer. L'objectif est de sélectionner la montagne la plus haute.

## Explication du Puzzle

Le jeu se déroule dans une boucle infinie (`while True`), où chaque itération représente un tour du jeu. Pendant chaque tour, vous recevez les hauteurs de huit montagnes différentes. Votre tâche est de déterminer la montagne la plus haute et d'indiquer son indice.

## Code Python

```python
import sys
import math

# La boucle while représente le jeu.
# Chaque itération représente un tour du jeu
# où vous recevez des entrées (les hauteurs des montagnes)
# et où vous devez afficher une sortie (l'indice de la montagne à attaquer)
# Les entrées que vous recevez sont automatiquement mises à jour en fonction de vos actions précédentes.

# Boucle de jeu
while True:
    plusGrand = 0
    cible = 0
    for i in range(8):
        montagne_h = int(input())  # représente la hauteur d'une montagne.
        if montagne_h > plusGrand:
            plusGrand = montagne_h
            cible = i

    # Écrire une action en utilisant print
    # Pour le débogage: print("Messages de débogage...", file=sys.stderr, flush=True)

    # L'indice de la montagne à attaquer.
    print(cible)
