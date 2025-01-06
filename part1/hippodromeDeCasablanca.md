## Hippodrome de Casablanca 


L’Hippodrome de Casablanca organise un nouveau type de course de chevaux : les duels. Lors d’un duel, seulement deux chevaux participent à la course. Pour que la course soit intéressante, il faut sélectionner deux chevaux qui ont une puissance similaire.

Écrivez un programme qui, à partir d’un ensemble donné de puissances, identifie les deux puissances les plus proches et affiche leur écart avec un nombre entier positif.

## Exemple
Entrée
3
5
8
9
Sortie
1

## Code
```python
import sys
import math

# Auto-generated code below aims at helping you parse
# the standard input according to the problem statement.

n = int(input())
powers = []
# enregistrer les puissances dans une liste
for i in range(n):
    pi = int(input())
    powers.append(pi)

#definition de la variable ecart
ecart = 100000

#double boucle pour verifier chaque element avec le reste des elements
for i in range(n):
    for j in range(n):
        if i != j:
            if abs(powers[i]  - powers[j]) < ecart:
                ecart = abs(powers[i]  - powers[j])
        
print(ecart)


```

