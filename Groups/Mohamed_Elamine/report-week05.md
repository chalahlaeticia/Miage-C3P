# Rapport – Semaine 5

## Introduction

J'ai bien aime le cours de la semaine derniere. Il portait sur la difference entre la delegation et l'heritage, et c'etait tres interessant !
. J'ai continue le jeu d'echecs en travaillant surtout sur les tests, suite au commentaire du prof ("in Tests we trust").

## Ce que j'ai fait

* J'ai implemente la prise en passant, avec 6 tests.
* J'ai termine le refactoring du rendu : avant, `MyChessSquare` avait une methode par type de piece. Maintenant, la case demande a la piece son rendu, et chaque piece donne juste sa table de lettres.
* J'ai corrige 3 bugs : le roi ne pouvait pas capturer, le pion n'attaquait pas ses diagonales, et il restait un test sur `nil` dans `MyKing`.


## Ce que j'ai appris

Dans mon projet, j'utilise l'heritage pour partager le comportement commun dans `MyPiece` : `MyPawn` redefinit `moveTo:` et appelle `super moveTo:`. J'utilise la delegation quand un objet confie un travail a un autre : le plateau envoie les clics a son etat (`MySelectedState` / `MyUnselectedState`), et la case delegue le rendu a la piece. L'heritage est pratique mais lie fortement les classes, la delegation est plus flexible. J'ai aussi vu qu'un test vert n'est pas toujours un bon test.

## Difficultes rencontrees

La prise en passant depend du coup precedent, donc il faut garder un etat sur le plateau et le remettre a zero au bon moment. Il fallait aussi choisir ou mettre la logique : j'ai choisi le pion.

## Conclusion

Le jeu est plus fiable. Il reste des limites : le roi peut capturer une piece defendue, et rien ne verifie qu'un coup ne met pas son propre roi en echec.


repo : https://github.com/amiineee863/PharoStuff
