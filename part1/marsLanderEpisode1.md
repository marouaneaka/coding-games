# Mars Lander

## Description du Puzzle

Le jeu simule une chute libre sur Mars sans atmosphère. Sur Mars, la gravité est de 3,711 m/s². En ajustant la puissance des fusées à une valeur X, on génère une poussée équivalente à X m/s² et on consomme X litres de carburant. Pour compenser la gravité martienne, une poussée quasi-verticale de 4 est nécessaire.

Pour qu'un atterrissage soit réussi, la capsule doit remplir les critères suivants :

- Atterrir sur un sol plat.
- Atterrir en position verticale (angle = 0°).
- Limiter la vitesse verticale (≤ 40 m/s en valeur absolue).
- Limiter la vitesse horizontale (≤ 20 m/s en valeur absolue).

## Le Code Python

```python
import sys
import math

# Le code auto-généré ci-dessous vise à vous aider à analyser
# l'entrée standard selon l'énoncé du problème.

surface_n = int(input())  # le nombre de points utilisés pour dessiner la surface de Mars.
for i in range(surface_n):
    # land_x : coordonnée X d'un point de surface. (0 à 6999)
    # land_y : coordonnée Y d'un point de surface. En reliant tous les points de manière séquentielle, on forme la surface de Mars.
    land_x, land_y = [int(j) for j in input().split()]

# Boucle de jeu
while True:
    # h_speed : la vitesse horizontale (en m/s), peut être négative.
    # v_speed : la vitesse verticale (en m/s), peut être négative.
    # fuel : la quantité de carburant restant en litres.
    # rotate : l'angle de rotation en degrés (-90 à 90).
    # power : la puissance de la poussée (0 à 4).
    x, y, h_speed, v_speed, fuel, rotate, power = [int(i) for i in input().split()]

    # Chaîne d'ordre pour le mouvement de la capsule
    chaine_ordre = ""
    if v_speed <= 10:
        chaine_ordre = "0 2"
        if y < 2000:
            chaine_ordre = "0 4"
    else:
        chaine_ordre = "0 0"

    # Affichage des deux entiers : rotation et puissance de la poussée.
    print(chaine_ordre)
