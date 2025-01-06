## Problème

Vous devez convertir un mot épelé à l'aide d'un alphabet phonétique d'une époque spécifique vers un autre alphabet phonétique.  
Les options sont de :
1. **Passer à l'alphabet suivant** si l'alphabet d'entrée n'est pas le plus récent (1956).
2. **Revenir au plus ancien alphabet** si l'alphabet d'entrée est déjà le plus récent.

---

## Exemple d'exécution

### Entrée
```
Authority Bills Capture
```

### Sortie
```
Apples Butter Charlie
```

---

## Code Python

```python

alphabets = {
    1908: [
        "Authority", "Bills", "Capture", "Destroy", "Englishmen", "Fractious", "Galloping", "High",
        "Invariably", "Juggling", "Knights", "Loose", "Managing", "Never", "Owners", "Play", "Queen",
        "Remarks", "Support", "The", "Unless", "Vindictive", "When", "Xpeditiously", "Your", "Zigzag"
    ],
    1917: [
        "Apples", "Butter", "Charlie", "Duff", "Edward", "Freddy", "George", "Harry", "Ink", "Johnnie",
        "King", "London", "Monkey", "Nuts", "Orange", "Pudding", "Queenie", "Robert", "Sugar", "Tommy",
        "Uncle", "Vinegar", "Willie", "Xerxes", "Yellow", "Zebra"
    ],
    1927: [
        "Amsterdam", "Baltimore", "Casablanca", "Denmark", "Edison", "Florida", "Gallipoli", "Havana",
        "Italia", "Jerusalem", "Kilogramme", "Liverpool", "Madagascar", "New-York", "Oslo", "Paris",
        "Quebec", "Roma", "Santiago", "Tripoli", "Uppsala", "Valencia", "Washington", "Xanthippe",
        "Yokohama", "Zurich"
    ],
    1956: [
        "Alfa", "Bravo", "Charlie", "Delta", "Echo", "Foxtrot", "Golf", "Hotel", "India", "Juliett",
        "Kilo", "Lima", "Mike", "November", "Oscar", "Papa", "Quebec", "Romeo", "Sierra", "Tango",
        "Uniform", "Victor", "Whiskey", "X-ray", "Yankee", "Zulu"
    ]
}


years = sorted(alphabets.keys())

def convert_word(word_list, current_year, target_year):
    current_alphabet = alphabets[current_year]
    target_alphabet = alphabets[target_year]
    converted = []
    for word in word_list:
        if word in current_alphabet:
            converted.append(target_alphabet[current_alphabet.index(word)])
    return converted


a_word_spelled_out = input().split()

# detection annee
current_year = None
for year, alphabet in alphabets.items():
    if a_word_spelled_out[0] in alphabet:
        current_year = year
        

if current_year == years[-1]:
    target_year = years[0]
else:
    target_year = years[years.index(current_year) + 1]

# Conversion
converted = convert_word(a_word_spelled_out, current_year, target_year)

if converted:
    print(" ".join(converted))

```

---

## Explication du Code

1. **Définition des alphabets** : Chaque alphabet phonétique est stocké sous forme de liste associée à une année dans un dictionnaire `alphabets`.

2. **Détection de l'année actuelle** : Le premier mot de l'entrée est comparé aux mots dans chaque alphabet pour identifier l'année d'origine.

3. **Détermination de l'année cible** :
   - Si l'année actuelle est la plus récente (`1956`), on choisit l'année la plus ancienne (`1908`).
   - Sinon, on passe à l'année suivante dans la liste triée `years`.

4. **Conversion des mots** : Les mots sont convertis de l'alphabet actuel vers l'alphabet cible en utilisant les indices.

5. **Affichage du résultat** : Les mots convertis sont affichés sous forme de chaîne.

---

## Tests

### Exemple 1
#### Entrée
```
Authority Bills Capture
```
#### Sortie
```
Apples Butter Charlie
```

### Exemple 2
#### Entrée
```
Alfa Bravo Charlie
```
#### Sortie
```
Amsterdam Baltimore Casablanca
```

### Exemple 3
#### Entrée
```
Apples Butter Charlie
```
#### Sortie
```
Amsterdam Baltimore Casablanca
```

---

![Validation des tests](img/natoAlpha.png)