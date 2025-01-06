## MIME Type

Le type MIME est utilisé dans de nombreux protocoles internet pour associer un type de média (html, image, vidéo, ...) avec le contenu envoyé. Ce type MIME est généralement déduit de l'extension du fichier à transférer.

Vous devez écrire un programme qui permet de détecter le type MIME d'un fichier à partir de son nom.
 	Règles
Une table qui associe un type MIME avec une extension de fichier vous est fournie. Une liste de noms de fichier à transférer vous sera aussi fournie et vous devrez déduire pour chacun d'eux, le type MIME à utiliser.

L'extension d'un fichier se définit par la partie du nom qui se trouve après le dernier point qui le compose.
Si l'extension du fichier est présente dans la table d'association (la casse ne compte pas. ex : TXT est équivalent à txt), alors affichez le type MIME correspondant . S'il n'est pas possible de trouver le type MIME associé à un fichier, ou si le fichier n'a pas d'extensions, affichez UNKNOWN.

## Exemple

### Entrée
2
4
html text/html
png image/png
test.html
noextension
portrait.png
doc.TXT

### Sortie
text/html
UNKNOWN
image/png
UNKNOWN
## Code
```python
import sys
import math

n = int(input())  # Nombre d'éléments constituant la table d'association.
q = int(input())  # Nombre Q de noms de fichiers à analyser.
extensions = {}

for i in range(n):
    # ext : extension de fichier
    # mt : type MIME
    ext, mt = input().split()
    extensions[ext.lower()] = mt  # en minuscules unifiées

for i in range(q):
    fname = input()  # Un nom de fichier par ligne.
    last_dot_index = fname.rfind('.')
    fname = fname.lower()  # en minuscules unifiées
    # Vérifier si un point est trouvé
    if last_dot_index != -1:
        # Extraire la sous-chaîne à partir du dernier point
        fname = fname[last_dot_index + 1:]
        if fname in extensions:
            print(extensions[fname])
        else:
            print("UNKNOWN")
    else:
        print("UNKNOWN")


```


