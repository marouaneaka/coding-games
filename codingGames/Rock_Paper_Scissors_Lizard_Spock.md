## Rock Paper Scissors Lizard Spock

Un tournoi international de Pierre-Papier-Ciseaux-Lézard-Spock est organisé, où chaque joueur reçoit un numéro lors de son inscription.

Chaque joueur choisit un signe qu'il conservera tout au long du tournoi parmi :
Pierre (P)
Papier (P)
Ciseaux (C)
Lézard (L)
Spock (S)

Les règles du jeu sont les suivantes :
Ciseaux coupent Papier
Papier couvre Pierre
Pierre écrase Lézard
Lézard empoisonne Spock
Spock écrase Ciseaux
Ciseaux décapitent Lézard
Lézard mange Papier
Papier contredit Spock
Spock vaporise Pierre
Pierre écrase Ciseaux
Et en cas d'égalité, le joueur avec le numéro le plus bas remporte la victoire (c'est scandaleux, mais c'est la règle).

## Exemple

    4 R \
        1 P \
    1 P /      \
                1 P
    8 P \      /     \
        8 P /       \
    3 R /              \
                        2 L
    7 C \              /
        5 S \       /
    5 S /      \     /
                2 L
    6 L \      /
        2 L /
    2 L /
    
The winner of the tournament is player 2. Before winning, he faced player 6, then player 5 and finally player 1.
   
## Code
```python
import sys
import math

# Nombre de joueurs dans le tournoi
n = int(input())

# Dictionnaire pour stocker les joueurs et leurs signes
tournament = {}
for i in range(n):
    inputs = input().split()
    numplayer = int(inputs[0])
    signplayer = inputs[1]
    tournament[numplayer] = signplayer

# Fonction pour déterminer le vainqueur d'un match entre deux joueurs
def match(p1, p2):
    rules = {
        "R": "LC",
        "P": "RS",
        "C": "PL",
        "L": "SP",
        "S": "CR"
    }
    if p2[1] in rules[p1[1]]:
        return p1
    elif p1[1] in rules[p2[1]]:
        return p2
    else:
        return min(p1, p2, key=lambda x: x[0])

# Fonction principale pour organiser le tournoi
def matchMaking(players):
    history = {}  # Dictionnaire pour stocker l'historique de chaque joueur
    while len(players) > 1:
        winners = {}

        # Match des joueurs par paires
        paired_players = list(players.items())
        for i in range(0, len(paired_players), 2):
            p1 = paired_players[i]
            p2 = paired_players[i + 1] if i + 1 < len(paired_players) else None

            if p2 is not None:
                winner = match(p1, p2)
                winners[winner[0]] = winner[1]

                # Enregistrement de l'historique de chaque joueur
                loser = p1 if winner == p2 else p2
                history[winner[0]] = loser[0]

        # Mise à jour des joueurs pour le tour suivant
        players = winners

    # Retourne le vainqueur final et l'historique du vainqueur final
    winner_key = list(players.keys())[0]
    return winner_key, history

# Exécution de la fonction principale pour obtenir le vainqueur final et son historique
winner, history = matchMaking(tournament)

# Affichage du vainqueur final
print(winner)

# Affichage de l'historique du vainqueur final
print(history[winner])


```
## Explication de la logique du code
La fonction matchMaking organise les matchs en paires, détermine les gagnants en fonction des règles du jeu (pierre-papier-ciseaux avec des signes spécifiques), et enregistre l'historique de chaque joueur à chaque étape. Le tournoi se poursuit jusqu'à ce qu'il ne reste qu'un seul joueur, désigné comme le vainqueur final. Le résultat affiche le numéro et le signe du vainqueur, ainsi que l'historique détaillé des matchs menant à sa victoire. Les règles du jeu, définies dans la fonction match, dictent les relations de victoire entre les différents signes des joueurs. 
