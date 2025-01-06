## Problème

Calculer la résistance équivalente d'un circuit constitué uniquement de résistances. Le circuit peut contenir des résistances en série ou en parallèle, notées respectivement avec des parenthèses `()` et des crochets `[]`.

### Définitions :
1. **Série** :  
   La résistance totale est la somme des résistances :  
   \( R_{eq} = R_1 + R_2 + \dots \)  
   Noté comme `( R_1 R_2 R_3 ... )`.

2. **Parallèle** :  
   La résistance totale est donnée par :  
   \( R_{eq} = \frac{1}{\frac{1}{R_1} + \frac{1}{R_2} + \dots} \)  
   Noté comme `[ R_1 R_2 R_3 ... ]`.

Le circuit peut être une combinaison de résistances en série et en parallèle.

### Entrée
- Un entier `N` : le nombre de résistances uniques dans le circuit.
- Les `N` lignes suivantes contiennent un nom et une valeur de résistance pour chaque résistance.
- Une ligne finale contenant la description du circuit avec les noms des résistances et leurs arrangements.

### Sortie
- La résistance équivalente du circuit, arrondie à la décimale la plus proche.

---

## Exemple d'exécution

### Entrée
```
2
A 20
B 10
( A B )
```

### Sortie
```
30.0
```

### Explication
- `( A B )` signifie que les résistances A et B sont en série.
- \( R_{eq} = 20 + 10 = 30.0 \).

---

## Code Python

```python
import sys

n = int(input().strip())
resistors = {}

for _ in range(n):
    name, r = input().strip().split()
    resistors[name] = int(r) 

circuit = input().strip()

def series_resistance(resistances):
    return sum(resistances)

def parallel_resistance(resistances):
    return 1 / sum(1 / r for r in resistances)

def evaluate(circuit):
    stack = []  
    i = 0
    while i < len(circuit):
        char = circuit[i]
        if char.isalnum():  # nom d'une resistance
            if char in resistors:  # verifie que le nom est dans le dictionnaire
                stack.append(resistors[char])
            else:
                raise KeyError(f"Résistance inconnue : {char}")
        elif char == '(':
            stack.append('(')
        elif char == ')':
            temp = []
            while stack and stack[-1] != '(':
                temp.append(stack.pop())
            if stack and stack[-1] == '(':
                stack.pop()  # Enlever le '('
            stack.append(series_resistance(temp[::-1]))
        elif char == '[':
            stack.append('[')
        elif char == ']':
            temp = []
            while stack and stack[-1] != '[':
                temp.append(stack.pop())
            if stack and stack[-1] == '[':
                stack.pop()  # Enlever le '['
            stack.append(parallel_resistance(temp[::-1]))
        i += 1
    return stack[0]


equivalent_resistance = evaluate(circuit)
print(f"{round(equivalent_resistance, 1):.1f}")


```

---

## Explication du Code

1. **Lecture des résistances** :  
   - Un dictionnaire `resistors` associe chaque nom de résistance à sa valeur.

2. **Évaluation récursive** :  
   - Le circuit est traité caractère par caractère :
     - Une résistance (nom) est remplacée par sa valeur.
     - Une parenthèse ouvrante `(` ou un crochet ouvrant `[` est ajoutée à une pile `stack`.
     - Lorsqu’une parenthèse ou un crochet fermant est rencontré, toutes les valeurs correspondantes sont récupérées, et leur résistance équivalente (en série ou en parallèle) est calculée.

3. **Série et parallèle** :  
   - Les fonctions `series_resistance` et `parallel_resistance` calculent la résistance équivalente pour un groupe donné.

4. **Résultat final** :  
   - La résistance équivalente est arrondie à la décimale la plus proche avant affichage.

---

## Tests

### Exemple 1
#### Entrée
```
2
A 20
B 10
( A B )
```
#### Sortie
```
30.0
```

### Exemple 2
#### Entrée
```
3
A 24
B 8
C 48
[ ( A B ) [ C A ] ]
```
#### Sortie
```
10.7
```