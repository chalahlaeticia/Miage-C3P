# Implémentation de l’en passant

## 1. Ce que j'ai fait

J'ai implémenté la gestion de la **prise en passant** pour les pions.

L'objectif était de permettre à un pion de détecter lorsqu'un pion adverse vient d'effectuer un déplacement de deux cases et qu'il peut donc être capturé en passant.

Pour pouvoir déterminer si un pion vient d'effectuer un déplacement de deux cases, j'ai ajouté la notion de **dernier déplacement (`lastMove`)**.

Dans un premier temps, j'ai essayé d'ajouter `lastMove` aux slots de `MyChessBoard`, afin que le plateau conserve le dernier déplacement effectué. Cela a provoqué plusieurs erreurs dans le package de tests et je n'ai pas réussi à déterminer précisément leur origine.

J'ai donc changé d'approche et décidé de conserver le dernier déplacement directement sur la pièce en ajoutant `lastMove` aux slots de `MyPiece`.

La méthode de déplacement a été adaptée afin d'enregistrer la case de départ et la case d'arrivée du pion lorsqu'il se déplace.

## 2. Découpage de l'implémentation

J'ai découpé la logique de la prise en passant en **plusieurs petites méthodes**, plutôt que de mettre toute la logique dans `targetSquaresLegal`. Cela permet de séparer les responsabilités.

### Recherche des cases adjacentes

J'ai créé des méthodes permettant de récupérer les cases situées à gauche et à droite du pion, puis les pions présents sur ces cases.

### Recherche des pions adverses

Une méthode permet ensuite d'identifier uniquement les pions appartenant à l'adversaire en utilisant la comparaison des couleurs.

### Vérification du déplacement de deux cases

J'ai séparé la vérification du déplacement initial en plusieurs étapes.

Le programme vérifie :

- la position initiale du pion ;
- sa position d'arrivée ;
- le fait que le déplacement corresponde bien à deux cases.

Les méthodes `startingFile`, `doubleMoveFile` et `madeDoubleMove` permettent donc de découper cette vérification.

### Détection des pions pouvant être capturés

Une méthode `canBeCapturedEnPassant` permet de déterminer si un pion peut être concerné par une prise en passant.

La méthode `enPassantPawns` utilise ensuite cette information pour sélectionner les pions adverses concernés.

### Calcul de la case de destination

J'ai également séparé le calcul de la case où le pion va effectuer la prise.

La méthode `forwardFrom` permet de calculer la case située devant un pion en fonction de sa couleur.

`enPassantSquareFor` utilise ensuite cette logique pour calculer la case de prise à partir du pion adverse.

Enfin, `enPassantSquaresFor` rassemble les différentes cases possibles.

### Intégration dans les déplacements légaux

Une fois cette logique séparée, il suffit d'ajouter les cases retournées par `enPassantSquaresFor` aux cases déjà calculées par `targetSquaresLegal`.

Ainsi, `targetSquaresLegal` reste principalement responsable de rassembler les différents types de déplacements possibles.

## 3. Pourquoi ce découpage ?

J'ai choisi cette implémentation pour **ne pas mettre toute la logique de la prise en passant dans une seule méthode** et pour factoriser le plus possible.

La prise en passant nécessite plusieurs vérifications différentes :

1. trouver les cases adjacentes ;
2. trouver les pions adverses ;
3. vérifier qu'ils viennent de faire un déplacement de deux cases ;
4. calculer la case de prise ;
5. ajouter cette case aux déplacements légaux.

J'ai donc essayé de faire correspondre chaque étape à une méthode.

Ce découpage rend le code plus facile à lire et permet également de tester les différentes parties séparément.

## 4. Tests réalisés

- `testPawnCanMoveEnPassant` : vérifie qu’une prise en passant est proposée lorsqu’un pion adverse vient d’effectuer un déplacement de deux cases.
- `testPawnCannotMoveEnPassantAfterOneSquareMove` : vérifie qu’une prise en passant n’est pas possible lorsqu’un pion adverse n’a avancé que d’une seule case.
- `testPawnCannotMoveEnPassantWithoutAdjacentPawn` : vérifie qu’une prise en passant n’est pas proposée lorsqu’aucun pion adverse n’est présent sur une case adjacente.
- `testPawnCannotMoveEnPassantAfterAnotherMove` : vérifie qu’une prise en passant ne devrait être possible que si le double déplacement du pion adverse correspond à son dernier déplacement.

## 5. Difficultés rencontrées

La principale difficulté a été de déterminer **où stocker l'information du dernier déplacement**.

J'ai d'abord essayé de mettre `lastMove` dans `MyChessBoard`, mais cela a provoqué des erreurs dans le package de tests que je n'ai pas réussi à résoudre.

J'ai donc choisi une autre solution : stocker le dernier déplacement dans la pièce elle-même.

Cette solution a permis de poursuivre l'implémentation et de faire passer le test principal de la prise en passant.

Une deuxième difficulté a été de gérer la prise en passant sans alourdir `targetSquaresLegal`.

La solution retenue a été de **découper progressivement la logique en petites méthodes**, chacune ayant une responsabilité précise.

Ce découpage a notamment permis de séparer :

- la recherche des cases adjacentes ;
- la recherche des pions adverses ;
- la vérification du double déplacement ;
- la détection d'un pion capturable en passant ;
- le calcul de la case de destination ;
- l'ajout final aux déplacements légaux.