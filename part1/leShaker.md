# Le Shaker 2023
Shaker : https://le-shaker.com/
# Sujet 1
## Dans de beaux draps
- Après avoir perdu vos compagnons dans la pénombre de la forêt, vous arrivez devant le gite, qui ressemble d'ailleurs plutôt à un manoir. Horreur et stupéfaction, la porte d'entrée est verrouillée ! C'est donc tout naturellement que vous entrez par la fenêtre de l'étage. Après tout, ça n'est pas une porte qui mettra fin à vos vacances
- Nouvel effroi : le rez-de-chaussée est rempli de fantômes !? Étant à l'étage, vous avez la brillante idée de les emprisonner en laissant tomber un grand drap sur eux. On donne la position de chaque fantôme sur une grille. Quelle est la surface minimale du drap permettant d'attraper tous les fantômes d'un coup? Un drap est carré et vous ne pouvez pas le faire tourner.
## Entrée

-Ligne 1: un entier N, le nombre de fantômes, 0 < N <= 1000
-Les N lignes suivantes : deux entiers Xi et Yi séparés par un espace, les coordonnées du i Eme fantôme, O <= Xi , Yi <= 1000
## Sortie
La surface minimale du drap carré permettant d'attraper tous les fantômes d'un coup.
# Solution
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
@author: mbelbella
"""

import sys


lines = []
for line in sys.stdin:
  lines.append(line.rstrip('\n'))
n = int(lines[0])

# On stock la valeur des xi xj et yi yj 
# On cherche le maximum entre xj xi et yj yi

MAX = 0
iteration = range(1,n+1)
for i in iteration:
    xi = int(lines[i].split()[0])
    yi = int(lines[i].split()[1])
    for j in iteration:
        xj = int(lines[j].split()[0])
        yj = int(lines[j].split()[1])
        dist = max(abs(xj-xi)+1,abs(yj-yi)+1)
        MAX = max(MAX,dist)
surface = MAX**2
print(surface)
