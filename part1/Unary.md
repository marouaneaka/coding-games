## Unary


Le binaire avec des 0 et des 1 c'est bien. Mais le binaire avec que des 0, ou presque, c'est encore mieux.

Ecrivez un programme qui, à partir d'un message en entrée, affiche le message codé avec cette technique en sortie.
  Règles

Voici le principe d'encodage :

    Le message en entrée est constitué de caractères ASCII (7 bits)
    Le message encodé en sortie est constitué de blocs de 0
    Un bloc est séparé d'un autre bloc par un espace
    Deux blocs consécutifs servent à produire une série de bits de même valeur (que des 1 ou que des 0) :
    - Premier bloc : il vaut toujours 0 ou 00. S'il vaut 0 la série contient des 1, sinon elle contient des 0
    - Deuxième bloc : le nombre de 0 dans ce bloc correspond au nombre de bits dans la série

## Exemple
Prenons un exemple simple avec un message constitué d'un seul caractère : C majuscule. C en binaire vaut 1000011 ce qui donne avec cette technique :

    0 0 (la première série composée d'un seul 1)
    00 0000 (la deuxième série composée de quatre 0)
    0 00 (la troisième série composée de deux 1)

C vaut donc : 0 0 00 0000 0 00
## Code
```python
import sys
import math

# Auto-generated code below aims at helping you parse
# the standard input according to the problem statement.

message = input()

encoded_message = ""
mbin = ''
# conversion en binaire
for c in message:
    mbin += bin(ord(c))[2:]

i = 0
while i < len(mbin):
    current_bit = mbin[i]
    count = 1

# compteur des bits succesifs avec la meme valeur
    while i < len(mbin) - 1 and mbin[i + 1] == current_bit:
          count += 1
          i += 1

    # codage du blic
    if current_bit == '0':
        encoded_message += '00 '
    else:
        encoded_message += '0 '

    # ajout des count bits
    encoded_message += '0' * count + ' '

    i += 1  # incrementation du i
# Write an answer using print
# To debug: print("Debug messages...", file=sys.stderr, flush=True)

print(encoded_message[:-1])

```
## Explication de la logique du code
1- conversion du message en binaire
2- on cree un pointeur i sur notre suite binaire et on compte avec count le nombre de bits succesifs avec la meme valeur
3- on commence notre codage
