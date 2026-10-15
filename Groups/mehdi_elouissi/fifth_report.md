# Rapport d'apprentissage – Semaine 5 : TDD avec le debugger et la prise en passant

## Introduction

Cette semaine, j'ai continué le chess game, mais en changeant ma façon de travailler. Au lieu de corriger le code directement, j'ai suivi le TDD (Test Driven Development) avec le debugger, comme on l'a vu dans le cours.

## Ce que j'ai fait

J'ai corrigé la **prise en passant**. J'ai commencé par écrire un test où un pion blanc avance de deux cases et se retrouve à côté d'un pion noir, puis je vérifie que le pion noir peut le prendre en passant.

Le test échouait, alors je l'ai lancé et j'ai utilisé le debugger pour voir où ça bloquait. J'ai pu corriger la méthode directement dans le debugger et relancer jusqu'à ce que le test passe. Avec ça, j'ai terminé le premier kata.

## Ce que j'ai appris

J'ai aussi pris du temps pour mieux lire la syntaxe de Pharo. J'ai trouvé un site qui l'explique bien : [cormas.org](https://cormas.org). Ça m'a aidé à mieux comprendre le syntax.

## Difficultés rencontrées

La prise en passant est plus compliquée que les autres règles du pion, parce qu'elle dépend du coup précédent de l'adversaire. Il fallait donc savoir quel pion venait d'avancer de deux cases, et pas seulement regarder la position actuelle.

## Conclusion

Le TDD avec le debugger est vraiment pratique en Pharo : on corrige le code pendant qu'il tourne au lieu de deviner où est le problème. Je pense continuer comme ça pour la suite du chess game.

Mon dépôt est toujours disponible ici : [pharo-tries](https://github.com/mehdi-elouissi/pharo-tries)