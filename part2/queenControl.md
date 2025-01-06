# Problème

Les échecs se jouent sur un plateau de 8x8 cases composé de 64 cases. Dans ce jeu, il est important de contrôler un grand nombre de ces cases pour prendre l'avantage sur l'adversaire. Une case est dite contrôlée lorsqu'elle se trouve dans le champ de mouvement d'une pièce d'échecs.

La pièce qui peut contrôler le plus de cases est la reine. Elle peut se déplacer verticalement, horizontalement et en diagonale.

**Mission :** Créez un programme capable de calculer le nombre de cases contrôlées par la reine à une position donnée.

Une case est considérée comme contrôlée lorsque la reine peut s'y déplacer.
- Une case contenant une pièce de la même couleur n'est pas considérée comme contrôlée.
- Une case contenant une pièce de la couleur opposée peut être considérée comme contrôlée.
- La case où se trouve actuellement la reine n'est pas comptée.

---

## Exemple

**Entrée**
```
white
Q.......
........
........
........
........
........
........
........
```

**Sortie**
```
21
```

---

## Code

```python
import sys


color = input()


board = [list(input()) for _ in range(8)]

def calculate_controlled_squares(board, color):
    # Calculer les cases contrôlées par les reines
    controlled_squares = 0

    # Directions possibles pour une reine (vertical, horizontal, diagonales)
    directions = [
        (-1, 0), (1, 0), (0, -1), (0, 1),  # Vertical et horizontal
        (-1, -1), (-1, 1), (1, -1), (1, 1) # Diagonales
    ]

    # Parcourir chaque case de l'échiquier
    for row in range(8):
        for col in range(8):
            if (color == "white" and board[row][col] == 'w') or (color == "black" and board[row][col] == 'b'):
                continue  # Ignorer les cases avec des pièces de la même couleur

            for direction in directions:
                i, j = row + direction[0], col + direction[1]

                while 0 <= i < 8 and 0 <= j < 8:
                    if board[i][j] == 'Q':
                        controlled_squares += 1
                        break  # La reine contrôle cette direction
                    elif board[i][j] != '.':
                        break  # Autre pièce bloquant la vue

                    i += direction[0]
                    j += direction[1]

    return controlled_squares

print(calculate_controlled_squares(board, color))
```

---

## Explication du code

1. **Lecture des données** :
   - La couleur de la reine ("white" ou "black") est lue en première ligne.
   - Les 8 lignes suivantes représentent l'état du plateau d'échecs, chaque ligne contenant 8 caractères (« . », « Q », « w » ou « b »).

2. **Calcul des cases contrôlées** :
   - Chaque case est vérifiée pour voir si elle est contrôlée par une reine, en fonction des règles du jeu d'échecs.
   - Les directions possibles pour le déplacement de la reine (8 directions) sont examinées.
   - Si une autre pièce est rencontrée dans une direction, la vue de la reine est bloquée dans cette direction.

3. **Règles d'exclusion** :
   - Les cases contenant des pièces de la même couleur que la reine sont ignorées.
   - La case actuelle de la reine n'est pas comptée.

4. **Affichage du résultat** :
   - Le nombre total de cases contrôlées est calculé et affiché en une seule ligne.

