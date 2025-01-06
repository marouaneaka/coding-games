## Encryption/Decryption of Enigma Machine
Pendant la Seconde Guerre mondiale, les Allemands utilisaient un code de cryptage appelé Enigma, essentiellement une machine de cryptage qui chiffrait des messages pour les transmettre. Le code Enigma est resté non décrypté pendant de nombreuses années. Voici comment fonctionne la machine de base :

Tout d'abord, une permutation de César est appliquée en utilisant un nombre croissant :
Si la chaîne est AAA et que le nombre de départ est 4, la sortie sera EFG.
A + 4 = E
A + 4 + 1 = F
A + 4 + 1 + 1 = G

Ensuite, la correspondance de EFG est effectuée avec le premier ROTOR, par exemple :
ABCDEFGHIJKLMNOPQRSTUVWXYZ
BDFHJLCPRTXVZNYEIWGAKMUSQO
Ainsi, EFG devient JLC. Ensuite, il passe à travers 2 rotors supplémentaires pour obtenir la valeur finale.

Si le deuxième ROTOR est AJDKSIRUXBLHWTMCQGZNPYFVOE, nous appliquons à nouveau l'étape de substitution comme suit :
ABCDEFGHIJKLMNOPQRSTUVWXYZ
AJDKSIRUXBLHWTMCQGZNPYFVOE
Donc, JLC devient BHD.

Si le troisième ROTOR est EKMFLGDQVZNTOWYHXUSPAIBRCJ, la substitution finale est :
ABCDEFGHIJKLMNOPQRSTUVWXYZ
EKMFLGDQVZNTOWYHXUSPAIBRCJ
Donc, BHD devient KQF.

La sortie finale est envoyée via un émetteur radio.

Entrée :
Ligne 1 : ENCODE ou DECODE
Ligne 2 : Décalage de départ N
Lignes 3-5 :
BDFHJLCPRTXVZNYEIWGAKMUSQO ROTOR I
AJDKSIRUXBLHWTMCQGZNPYFVOE ROTOR II
EKMFLGDQVZNTOWYHXUSPAIBRCJ ROTOR III
Ligne 6 : Message à coder ou décoder

Sortie :
Chaîne encodée ou décodée
## Code
```python
import sys
import math

# Auto-generated code below aims at helping you parse
# the standard input according to the problem statement.

operation = input()
pseudo_random_number = int(input())
rotors = []

# fonction qui cree un dictionnaire pour tous les rotors selon deux strings
def map(string1, string2):
    return {char1: char2 for char1, char2 in zip(string1, string2)}


#cette fonction incremente le caractere par un nombre ;
def incremente(message,pseudo_random_number,methode):
    tmp = ''
    if methode == 'ENCODE':
        for i,A in enumerate(message):
           rotate = pseudo_random_number+i
           # ORD DE Z EST 90 ET DE A EST 65, 
           if ord(A) + rotate > 90:
               newCode = (ord(A) + rotate)-90+64
               if newCode > 90:
                   tmp += chr(newCode - 90 + 64 ).upper()
               else:
                   tmp += chr(newCode).upper()
           else:
               tmp += chr(ord(A)+rotate).upper()
    elif methode == 'DECODE':
        for i, A in enumerate(message):
            rotate = pseudo_random_number + i
            # ORD DE A EST 65 ET DE Z EST 90,
            if ord(A) - rotate < 65:
                new_code = 90 - (65 - (ord(A) - rotate)) + 1
                if new_code < 65:
                    tmp += chr(new_code + 90 - 65 + 1).upper()
                else:
                    tmp += chr(new_code).upper()
            else:
                tmp += chr(ord(A) - rotate).upper()
    return tmp

for i in range(3):
    rotor = input()
    #creation des rotors
    rotors.append(map("ABCDEFGHIJKLMNOPQRSTUVWXYZ",rotor))
message = input()


# CODAGE DECODAGE
if (operation == "ENCODE"):
    tmp = incremente(message,pseudo_random_number,'ENCODE')
    #ROTORS :
    tmpA = [3]
    tmpA[0] = tmp
    for i in range(3):
        # on charge les rotors de la memoire
        rotorN = rotors[i]
        tmp=""
        for c in tmpA[i]:
            if c.isupper() and c in rotorN:
               tmp += rotorN[c]
            else:
               tmp += c
        tmpA.append(tmp)
    res = tmpA[3]
else:
    #inverser les ROTORS :
    tmp2 = message 
    for i in range(2,-1,-1):
        # on charge les rotors de la memoire
        rotorN = rotors[i]
        tmp = ""
        for c in tmp2:
            tmp += next(key for key, value in rotorN.items() if value == c)
        tmp2 = tmp
    #inverser le pseudo  random number
    res = incremente(message, pseudo_random_number, "DECODE")


print(res)
```
## Explication de la logique du code
la fonction Map : 
 prend deux chaînes de caractères et crée un dictionnaire où chaque caractère de la première chaîne est associé au caractère correspondant dans la deuxième chaîne.
La fonction incremente :
 prend un message, un nombre pseudo-aléatoire et une méthode (ENCODE ou DECODE) pour incrémenter (chiffrer) ou décrémenter (déchiffrer) chaque caractère du message en fonction de la méthode spécifiée.
Boucle des rotors : 
 demande à l'utilisateur de fournir les configurations des trois rotors, puis crée un dictionnaire de mappage pour chaque rotor en utilisant la fonction map et les ajoute à la liste rotors.
Bloc ENCODE :
 effectue l'encodage du message en utilisant les rotors et le nombre pseudo-aléatoire. Il stocke les résultats intermédiaires dans la liste tmpA et le résultat final dans res.

La partie de DECODAGE n'est pas encore parfaite
