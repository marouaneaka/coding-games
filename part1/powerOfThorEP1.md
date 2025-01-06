# Power of Thor - Episode 1

## Description du Puzzle

Dans ce puzzle, vous devez guider Thor, le dieu du tonnerre, vers la position de la source de pouvoir en utilisant des commandes directionnelles. Thor peut se déplacer dans huit directions différentes : N (nord), NE (nord-est), E (est), SE (sud-est), S (sud), SW (sud-ouest), W (ouest) ou NW (nord-ouest). La source de pouvoir est représentée par une lumière, et Thor doit ajuster sa position pour s'en approcher.

## Le Code Python

```python
import sys
import math

# Le code auto-généré ci-dessous vise à vous aider à analyser
# l'entrée standard selon l'énoncé du problème.

# light_x : la position X de la lumière de pouvoir
# light_y : la position Y de la lumière de pouvoir
# initial_tx : position X initiale de Thor
# initial_ty : position Y initiale de Thor
light_x, light_y, initial_tx, initial_ty = [int(i) for i in input().split()]

# Boucle de jeu
while True:
    remaining_turns = int(input())  # Le nombre restant de tours que Thor peut effectuer. Ne supprimez pas cette ligne.
    
    # Initialisation du poids de déplacement
    poids = 1
    if remaining_turns < 20:
        poids = 1

    # Conditions pour déterminer la direction de déplacement de Thor
    if light_y > initial_ty and light_x > initial_tx:
        print("SE")
        initial_ty += poids
        initial_tx += poids
    if light_y > initial_ty and light_x < initial_tx:
        print("SW")
        initial_ty += poids
        initial_tx -= poids
    if light_y < initial_ty and light_x > initial_tx:
        print("NE")
        initial_ty -= poids
        initial_tx += poids
    if light_y < initial_ty and light_x < initial_tx:
        print("NW")
        initial_ty -= poids
        initial_tx -= poids
    if initial_tx == light_x and initial_ty > light_y:
        initial_ty -= poids
        print("N")
    if initial_tx == light_x and initial_ty < light_y:
        initial_ty += poids
        print("S")
    if initial_tx > light_x and initial_ty == light_y:
        initial_tx -= poids
        print("W")
    if initial_tx < light_x and initial_ty == light_y:
        initial_tx += poids
        print("E")
