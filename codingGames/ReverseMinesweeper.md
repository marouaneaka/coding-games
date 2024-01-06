## ReverseMine Sweeper

Étant donné une grille d'emplacement de mines (où les '.' sont des cellules vides et les 'x' sont des mines), votre objectif est d'afficher la grille telle qu'elle apparaît si vous remportez le jeu.
Chaque position est un chiffre indiquant le nombre de mines qui la bordent (y compris les diagonales). Les mines (x) n'apparaissent plus. Les mines et les positions qui ne bordent aucune mine apparaissent tous deux comme des cellules vides (.).
Entrée
Ligne 1 : un entier w pour la largeur de la grille.
Ligne 2 : un entier h pour la hauteur de la grille.
Les h lignes suivantes : chaque ligne du champ de mines, avec des points (.) ou des mines (x).
Sortie
h lignes de largeur w montrant le jeu de démineur terminé.
Contraintes
1 <= w <= 30
1 <= h <= 30

## Exemple

Entrée

16
9
................
................
................
................
................
....x...........
................
................
................

Sortie

................
................
................
................
...111..........
...1.1..........
...111..........
................
................
## Code
```python
import sys
import math

def count_mines(grid, x, y, h, w):
    directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]
    compteur = 0
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < h and 0 <= ny < w and grid[nx][ny] == 'x':
            compteur += 1
    return compteur

def initialize_grid(w, h):
    return [['.' for _ in range(w)] for _ in range(h)]

def update_grid_with_mines(grid, plateau, h, w):
    for i in range(h):
        for j in range(w):
            if plateau[i][j] != 'x':
                mines_count = count_mines(plateau, i, j, h, w)
                if mines_count > 0:
                    grid[i][j] = str(mines_count)
    return grid

def print_grid(grid):
    for row in grid:
        print(''.join(row))

if __name__ == "__main__":
    w = int(input())
    h = int(input())

    plateau = [input() for _ in range(h)]

    grille = initialize_grid(w, h)

    grille = update_grid_with_mines(grille, plateau, h, w)

    print_grid(grille)


```
## Explication de la logique du code
Ce code est une implémentation en Python du jeu de démineur. Voici une explication détaillée du code :

1. **Fonction `count_mines` :**
   - Cette fonction prend en paramètres la grille de jeu (`grid`), les coordonnées d'une cellule spécifique (`x` et `y`), ainsi que les dimensions de la grille (`h` pour la hauteur et `w` pour la largeur).
   - Elle compte le nombre de mines autour de la cellule spécifiée en utilisant les directions définies dans la liste `directions`. Pour chaque direction, elle vérifie si la cellule adjacente contient une mine ('x').
   - Le compteur est incrémenté chaque fois qu'une mine est trouvée.
   - La fonction retourne le nombre total de mines autour de la cellule spécifiée.

2. **Fonction `initialize_grid` :**
   - Cette fonction prend en paramètres la largeur (`w`) et la hauteur (`h`) de la grille.
   - Elle initialise une grille vide de dimensions `h` x `w` remplie de points ('.').

3. **Fonction `update_grid_with_mines` :**
   - Cette fonction prend en paramètres la grille à mettre à jour (`grid`), le plateau de jeu initial (`plateau`), ainsi que les dimensions de la grille (`h` et `w`).
   - Elle parcourt chaque cellule du plateau (`plateau`) et met à jour la grille (`grid`) avec le nombre de mines adjacentes à chaque cellule non-mine.
   - Si une cellule contient une mine, elle ne fait rien.
   - La fonction retourne la grille mise à jour.

4. **Fonction `print_grid` :**
   - Cette fonction prend en paramètre une grille (`grid`) et l'affiche ligne par ligne.
   - Elle utilise `print(''.join(row))` pour imprimer chaque ligne de la grille sans espaces entre les caractères.

5. **Bloc principal (`if __name__ == "__main__":`) :**
   - Il lit la largeur et la hauteur de la grille depuis l'entrée standard (`input()`).
   - Il lit chaque ligne du plateau de jeu (`plateau`) à partir de l'entrée standard.
   - Il initialise une grille vide (`grille`) à l'aide de la fonction `initialize_grid`.
   - Il met à jour la grille avec le nombre de mines adjacentes à l'aide de la fonction `update_grid_with_mines`.
   - Il affiche la grille résultante à l'aide de la fonction `print_grid`.
