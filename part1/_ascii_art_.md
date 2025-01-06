# Art ASCII

## Description du Puzzle

Le défi consiste à écrire un programme capable d'afficher une ligne de texte en art ASCII dans un style spécifié en entrée.

## Le Code Python

```python
import sys
import math

l = int(input())
h = int(input())
t = input()

ascii_chars = [input() for _ in range(h)]

t = t.upper()

for i in range(h):
    line_ascii = ""

    for char in t:
        if 'A' <= char <= 'Z':
            char_index = ord(char) - ord('A')
        else:
            char_index = 26

        char_ascii = ascii_chars[i][char_index * l:(char_index + 1) * l]

        line_ascii += char_ascii

    print(line_ascii)
