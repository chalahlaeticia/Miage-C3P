# Rapport Semaine 4

## Hammed ABASS

Cette semaine, j'ai travaillé sur l'exercice FS de la semaine dernière avant de commencer le projet d'échecs.

Je viens de commencer le jeu d'échecs. J'ai passé du temps à lire le code pour comprendre comment les classes fonctionnent ensemble. En plus de Pharo, je dois aussi apprendre les règles des échecs, parce que je ne savais pas y jouer. Par exemple, je ne savais pas que les pawns ne capturent pas dans la même direction qu'ils avancent.

J'ai commencé par corriger les déplacements des pawns et un doublon dans les déplacements du bishop. J'ai aussi utilisé le Null Object vu en cours pour les cases vides, avec `MyNoPiece` à la place de `nil`.

Un autre problème était qu'un coup refusé pouvait quand même être ajouté à l'historique. J'ai corrigé ça ainsi que le changement de joueur : si le coup ne passe pas, le joueur garde son tour.

J'ai ajouté et revu des tests pour ces corrections, en regroupant les cas qui se répétaient. J'essaie de faire attention à ce que les tests servent vraiment à trouver un problème.

Je commence à mieux me repérer dans Pharo et à comprendre le code. Faire le lien avec ce que je connais en Java ou en TypeScript m'aide à avancer.

[Mon dépôt ChessPharo](https://github.com/AbassHammed/ChessPharo)

---

## Julie LIM

Pour cette 4ème semaine, j'ai commencé par essayer de comprendre le fonctionnement du projet Chess avant de modifier le code

J'ai parcouru plusieurs classes comme MyChessGame, MyPlayer, MySelectedState et MyUnselectedState afin de comprendre comment les déplacements et les changements de joueur étaient gérés

En testant le jeu manuellement, j'ai remarqué qu'il était possible de jouer plusieurs fois avec le même joueur
J'ai donc essayé de suivre le chemin du code lors d'un clic sur une pièce et d'un déplacement

J'ai corrigé ce problème en ajoutant une vérification de la couleur de la pièce par rapport au joueur courant puis en ajoutant le changement de joueur après un déplacement manuel

J'ai également commencé à regarder d'autres comportements incorrects, notamment certains clics qui peuvent être interprétés comme des déplacements alors que la pièce n'a pas réellement bougé

Pour le moment, je n'ai corrigé qu'un bug et il reste encore plusieurs problèmes dans le jeu que je dois analyser et corriger
