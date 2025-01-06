
## Problème

Le jeu **Six Degrees of Kevin Bacon** consiste à relier un acteur donné à Kevin Bacon à travers les films dans lesquels ils ont joué. Chaque connexion est basée sur un film commun où deux acteurs ont travaillé ensemble.

Dans ce problème, on doit déterminer le **Bacon number** d'un acteur, c'est-à-dire le **nombre minimal de films nécessaires pour relier cet acteur à Kevin Bacon**.

### Entrée

1. **Ligne 1** : `actor_name`, le nom de l'acteur pour lequel le Bacon number est calculé.
2. **Ligne 2** : Un entier `n`, représentant le nombre de films donnés.
3. **Lignes suivantes** : `n` chaînes de texte, chaque chaîne au format :
   ```
   Movie_name: Actor 1, Actor 2, ..., Actor k
   ```

### Sortie

Une seule ligne contenant un entier : le **Bacon number** de `actor_name`.

### Contraintes

- Il existe toujours un chemin vers Kevin Bacon.
- \( 0 < n < 50 \)
- Chaque film contient au maximum 10 acteurs.
- Les noms des films et des acteurs sont séparés respectivement par `: ` et `, `.

---

## Exemple d'exécution

### Exemple 1

#### Entrée
```
Elvis Presley
3
Change of Habit: Elvis Presley, Mary Tyler Moore, Barbara McNair, Jane Elliot, Ed Asner
JFK: Kevin Costner, Kevin Bacon, Tommy Lee Jones, Laurie Metcalf, Gary Oldman, Ed Asner
Sleepers: Kevin Bacon, Jason Patric, Brad Pitt, Robert De Niro, Dustin Hoffman
```

#### Sortie
```
2
```

#### Explication

1. **Acteurs connectés** :
   - Elvis Presley joue avec Ed Asner dans *Change of Habit*.
   - Ed Asner joue avec Kevin Bacon dans *JFK*.
2. **Bacon number** : 2 films.

---

## Code Python

```python
from collections import defaultdict, deque

actor_name = input().strip()
n = int(input().strip())

#graphe d'acteurs à partir des films
graph = defaultdict(set)
for _ in range(n):
    movie_cast = input().strip()
    _, cast = movie_cast.split(": ")
    actors = cast.split(", ")
    for actor in actors:
        for co_actor in actors:
            if actor != co_actor:
                graph[actor].add(co_actor)

# trouver le Bacon number avec un parcours BFS
def find_bacon_number(graph, start_actor, target_actor="Kevin Bacon"):
    visited = set()
    queue = deque([(start_actor, 0)])  # (acteur actuel, distance actuelle)

    while queue:
        current_actor, degree = queue.popleft()
        if current_actor == target_actor:
            return degree
        if current_actor not in visited:
            visited.add(current_actor)
            for neighbor in graph[current_actor]:
                queue.append((neighbor, degree + 1))
    

bacon_number = find_bacon_number(graph, actor_name)
print(bacon_number)
```

---

## Explication du Code

1. **Construction du graphe** :
   - Chaque acteur est un nœud du graphe.
   - Une arête existe entre deux acteurs s'ils ont joué dans le même film.
   - Utilisation d'un dictionnaire `graph` où chaque clé est un acteur et la valeur est l'ensemble des acteurs avec lesquels il a travaillé.

2. **Recherche avec BFS** :
   - On utilise une **file (deque)** pour parcourir le graphe en largeur.
   - Chaque acteur visité est marqué pour éviter les cycles.
   - La distance (ou le degré de séparation) est incrémentée à chaque saut entre acteurs.

3. **Complexité** :
   - **Temps** : \( O(V + E) \), où \( V \) est le nombre d'acteurs et \( E \) le nombre de relations.
   - **Espace** : \( O(V) \) pour stocker les acteurs visités et la file.

---

## Tests
![Validation des tests](img/kevinBacon.png)
```