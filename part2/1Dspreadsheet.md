# Problème
Vous disposez d'une feuille de calcul unidimensionnelle. Vous devez résoudre les formules et donner la valeur de toutes ses cellules.

Le contenu de chaque cellule d'entrée est fourni sous forme d'une opération avec deux opérandes, arg1 et arg2.

Il existe 4 types d'opérations :
- **VALUE arg1 arg2** : La valeur de la cellule est arg1 (arg2 n'est pas utilisé et sera "_" pour aider à l'analyse).
- **ADD arg1 arg2** : La valeur de la cellule est arg1 + arg2.
- **SUB arg1 arg2** : La valeur de la cellule est arg1 - arg2.
- **MULT arg1 arg2** : La valeur de la cellule est arg1 × arg2.

Les arguments peuvent être de deux types :
- **Référence $ref** : Si un argument commence par un signe dollar, il est interprété comme une référence et sa valeur est égale à la valeur de la cellule de ce numéro ref, indexé à partir de 0. Par exemple, "$0" aura la valeur du résultat de la première cellule.
  - Une cellule peut référencer une cellule postérieure !
- **Valeur val** : Si un argument est un nombre pur, sa valeur est val. Par exemple : "3" aura la valeur 3.

Il n'y aura pas de références cycliques : une cellule ne peut pas se référencer elle-même ou une cellule qui la référence, directement ou indirectement.

### Entrée
- Ligne 1 : Un entier N pour le nombre de cellules.
- Les N lignes suivantes : operation arg1 arg2

  - **operation** est l'une des suivantes : { VALUE, ADD, SUB, MULT }
  - **arg1** et **arg2** sont soit un nombre ("-?[0-9]+"), une référence ("\$[0-9]+"), ou rien "_".

### Sortie
N lignes : la valeur de chaque cellule, une valeur par ligne, de la cellule 0 à la cellule N.

### Contraintes
- 1 ≤ N ≤ 100
- -10000 ≤ val ≤ 10000
- $0 ≤ $ref ≤ $(N-1)
- val ∈ ℤ
- ref ∈ ℕ
- Il n'y a pas de références cycliques.

### Exemple
**Entrée**
```
2
VALUE 3 _
ADD $0 4
```
**Sortie**
```
3
7
```

---

# Exemple de code
```python
import sys

# Définition des types d'opérations
# Ces constantes représentent les opérations prises en charge pour la feuille de calcul
VALUE = "VALUE"
ADD = "ADD"
SUB = "SUB"
MULT = "MULT"

def parse_argument(arg, cells, evaluated):
    # Analyse un argument pour obtenir une valeur numérique ou évaluer une cellule référencée
    if arg == "_":
        return 0  # Valeur par défaut pour les arguments vides
    elif arg.startswith("$"):
        # si l'argument est une référence à une autre cellule, évaluer cette cellule
        return evaluate_cell(int(arg[1:]), cells, evaluated)
    else:
        # retourner la valeur entière de l'argument
        return int(arg)

def evaluate_cell(index, cells, evaluated):
    
    if index in evaluated:
        return evaluated[index]  

    operation, arg1, arg2 = cells[index]  # détails de la cellule

    # opération en fonction du type
    if operation == VALUE:
        result = parse_argument(arg1, cells, evaluated)
    elif operation == ADD:
        result = parse_argument(arg1, cells, evaluated) + parse_argument(arg2, cells, evaluated)
    elif operation == SUB:
        result = parse_argument(arg1, cells, evaluated) - parse_argument(arg2, cells, evaluated)
    elif operation == MULT:
        result = parse_argument(arg1, cells, evaluated) * parse_argument(arg2, cells, evaluated)

    
    evaluated[index] = result
    return result

n = int(input())


cells = [tuple(input().split()) for _ in range(n)]


evaluated = {}
for i in range(n):
    print(evaluate_cell(i, cells, evaluated))
```

---

# Explication du code

1. **Définition des constantes et fonctions** :
   - Les opérations VALUE, ADD, SUB, et MULT sont définies comme des constantes.
   - `parse_argument` permet de traduire les arguments (valeurs ou références).
   - `evaluate_cell` évalue la valeur d'une cellule en fonction de son opération et de ses arguments.

2. **Lecture des données** :
   - Le nombre de cellules est lu en premier.
   - Les détails de chaque cellule (opération, arg1, arg2) sont stockés sous forme de tuples.

3. **Évaluation des cellules** :
   - Les cellules sont évaluées dans l'ordre. Si une cellule référence une autre, celle-ci est évaluée récursivement.
   - Les résultats sont mis en cache pour éviter de recalculer plusieurs fois la même cellule.

4. **Affichage des résultats** :
   - Une fois évaluées, les valeurs des cellules sont affichées dans l'ordre.

Ce code garantit une gestion efficace des références et des opérations dans une feuille de calcul unidimensionnelle.

