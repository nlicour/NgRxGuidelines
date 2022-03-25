# Choisir son opérator

|Operateur | desc |
|---|---|
|switchMap| Annule la requête courante s'il y a une 2eme demande en cours.|
|concatMap| Lance les demandes dans l'ordre. (Perte de performances)|
|mergeMap| Lance toutes les demandes en //|
|exhaustMap| Ignore toutes les autres demandes pendant que la requête est en cours |

