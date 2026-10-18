# Rapport du TP Chess

## Introduction

L’objectif de ce TP était de travailler sur un projet existant en Pharo à travers plusieurs katas portant sur les tests, le débogage, le refactoring, le polymorphisme et les design patterns.

J’ai commencé par le kata **Fix pawn moves**, car il permettait de comprendre le fonctionnement du jeu avec une première correction simple. J’ai suivi la démarche **TDD** (*Test-Driven Development*) :

1. écrire un test qui montre le problème ;
2. modifier le code ;
3. relancer le test pour vérifier la correction.

---

## Kata 1 — Fix pawn moves

### Objectif

Le premier objectif était de corriger le déplacement initial du pion. Un pion peut avancer de deux cases uniquement lorsqu’il se trouve sur son rang de départ et lorsque les deux cases devant lui sont libres.

- Le pion blanc commence sur le rang `2` et monte.
- Le pion noir commence sur le rang `7` et descend.

### Commit 1 — Correction du déplacement initial de deux cases

**Commit :** `ddc551b`

J’ai d’abord ajouté un test qui place un pion blanc en `e2` et vérifie que les cases `e3` et `e4` sont proposées comme déplacements possibles.

J’ai ensuite modifié la méthode `MyPawn >> targetSquaresLegal , :`

j’ai utilisé deux variables :

- `first` représente la première case devant le pion ;
- `second` représente la deuxième case devant le pion.
pour :

- calculer la première et la deuxième case devant le pion ;
- prendre en compte sa couleur et sa direction ;
- vérifier qu’il se trouve sur son rang initial ;
- vérifier que les deux cases sont libres.

### Lien avec le cours

Ce commit m’a permis d’appliquer :

- la démarche **TDD** ;
- les tests unitaires ;
- les blocs conditionnels ;
- les collections Pharo ;
- le débogage progressif.

### Résultat

Le pion peut maintenant avancer d’une ou de deux cases depuis sa position initiale lorsque le chemin est libre.

### Commit 2 — Ajout des tests de restriction du déplacement

**Commit :** `347d49d`

Après avoir ajouté le déplacement initial de deux cases, j’ai complété les tests pour vérifier les restrictions de ce déplacement.

Deux situations sont maintenant testées :

- un pion blanc placé en `e2` peut avancer vers `e3` et `e4` si le chemin est libre ;
- si la case `e4` est occupée, elle ne doit pas apparaître dans les déplacements possibles.

J’ai également regroupé ces tests dans la classe `MyPawnTest` afin de garder une seule classe de test pour le pion.


### Commit 3 — Correction de la capture diagonale du pion

**Commit :** `1901ea1`

Le pion ne se déplace pas de la même manière lorsqu’il avance et lorsqu’il capture une pièce. Il avance verticalement, mais capture uniquement en diagonale.

J’ai ajouté la méthode `captureSquares` pour séparer le calcul des captures du déplacement normal.

Cette méthode calcule les deux cases diagonales selon la couleur :

- `up left` et `up right` pour un pion blanc ;
- `down left` et `down right` pour un pion noir.

Une case diagonale est retenue uniquement si :

- elle existe sur le plateau ;
- elle contient une pièce ;
- cette pièce possède une couleur différente.

Les cases trouvées par `captureSquares` sont ensuite ajoutées aux déplacements possibles du pion.

### Test ajouté

J’ai placé un pion blanc en `e4` et un pion noir en `f5`. Le test vérifie que `f5` appartient aux cases accessibles par le pion blanc.


### Résultat

Le pion peut maintenant capturer une pièce adverse située sur une case diagonale.

### Commit 4 — Correction de la capture du pion au bord de l’échiquier

**Commit :** `e3ac03d`

Après avoir ajouté la capture diagonale, j’ai remarqué un problème quand le pion se trouvait au bord du plateau.

Le code calculait directement les diagonales avec `square up left` ou `square down right`. Si la première case calculée était en dehors du plateau, le résultat était `nil` et Pharo essayait ensuite de lui envoyer le message `left` ou `right`.

### Approche suivie

J’ai séparé le calcul en deux étapes :

- calculer d’abord la case devant le pion ;
- calculer ensuite les diagonales seulement si cette case existe.

Pour cela, j’ai utilisé `ifNotNil:` avant d’envoyer les messages `left` et `right`.

### Test ajouté

Aucun nouveau test n’a été ajouté dans ce commit. Le test du cas limite a été ajouté dans le commit suivant pour vérifier que le problème ne revient pas.

### Commit 5 — Ajout d’un test pour le pion au bord de l’échiquier

**Commit :** `fa64ad0`

Après avoir corrigé le problème de capture au bord du plateau, j’ai ajouté un test pour protéger cette correction.




