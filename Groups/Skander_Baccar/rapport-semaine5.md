# Rapport – Semaine 5

Cette semaine, j'ai travaillé sur deux katas du jeu d'échecs https://github.com/skanderBCA14/Chess, en TDD et par petites étapes, avec un commit à chaque étape. Au fur et à mesure, j'ai relu les cours et les vidéos du MOOC pour choisir la bonne technique à chaque fois. Un de mes objectifs était d'éviter les `if` au maximum : laisser les objets décider grâce au polymorphisme, aux dispatchs et aux collections.

## Kata 1 : Fix pawn moves (terminé)

J'ai écrit `MyPawnTest` avant de toucher au code, l'avance d'une ou deux cases, le chemin bloqué, la prise en diagonale uniquement, la prise en passant et la promotion. De petites méthodes d'aide (`put:at:`, `pieceAt:`…) gardent les tests courts et lisibles. J'ai aussi ajouté des tests de garde (pions noirs, bord de l'échiquier, prise en passant contre une autre pièce) pour éviter les régressions.

**Le code :**
- **Petites méthodes** : chaque règle a sa propre méthode (`canDoubleStep`, `isOnStartingRank`, `captureSquares`…), ce qui rend le code facile à lire et à réutiliser.
- **Objets plutôt que données** : les cases se calculent avec des `Point` (`square + forwardDirection`), sans manipuler des coordonnées à la main.
- **Création côté classe** : `MyPawn white` et `MyPawn black` donnent sa direction au pion dès sa création, donc il ne vérifie plus sa couleur.
- **Template Method** : `MyPiece >> moveTo:` vérifie que le coup est légal, puis appelle `performMoveTo:`. `MyPawn` redéfinit seulement `performMoveTo:` pour ajouter la prise en passant, et appelle `super` pour garder le déplacement normal.
- **Null Object** pour la prise en passant : l'échiquier doit se souvenir si une prise en passant est possible. Au lieu de mettre nil quand elle ne l'est pas et de le vérifier partout, il garde un objet `MyNoEnPassant` qui répond toujours « non ». Après un coup de pion, il le remplace par un `MyEnPassant`, qui retient le pion qui vient de jouer et la case qu'il a sautée, et qui répond « oui » si ce pion a avancé de deux cases. Le pion qui veut prendre pose toujours la même question sans savoir à qui il parle, ce qui évite les if et les nil.
- **Promotion au choix** : `moveTo:promotingTo:` permet de choisir la pièce, et chaque choix a son propre test.
- **Itérateurs plutôt que `if`** : `select:` et `do:` sur de petites collections. Quand la condition est fausse, la collection est simplement vide.
- **Le seul `if` gardé dans ce que j'ai écrit** : `moveTo:` garde un `ifFalse:` pour refuser un coup illégal. Comme c'était une simple condition, je l'ai laissée exprès, le code est plus clair ainsi.

**La prise en passant en jeu.** Si un pion avance de deux cases et arrive à côté d'un pion adverse, ce dernier peut le prendre en allant en diagonale sur la case sautée, mais seulement au coup suivant. Pour la tester : e2-e4, a7-a6, e4-e5, d7-d5, puis e5-d6. Le pion noir en d5 disparaît.

## Kata 2 : Refactor piece rendering (en cours)

À l'origine, l'affichage reposait sur six méthodes presque identiques (`renderKnight:`, `renderQueen:`…) avec du code dupliqué.

- **Tests de caractérisation** : avant de refactoriser, j'ai écrit `MyPieceRenderingTest`, qui fige les quatre lettres de chaque pièce. Ces tests doivent rester verts pendant tout le refactoring.
- **Hooks** : `MyPiece` déclare `whiteLetter` et `blackLetter`, et chaque pièce les définit (**dispatch simple** sur la classe de la pièce, sans `if`).
- **Table dispatch** : une table associe la couleur de la pièce à sa lettre, et une autre table associe la couleur de la case à un petit bloc qui met la lettre en minuscule quand la case est sombre. Les deux `if` imbriqués de chaque méthode disparaissent.

**Double dispatch ?** Oui, c'est possible, et le code d'origine en fait déjà une partie (la pièce appelle `renderKnight:` sur la case). Mais pour enlever aussi les `if` sur les couleurs, il faudrait créer des classes pour chaque couleur de pièce et de case, avec environ une vingtaine de méthodes.

**Table dispatch ?** Oui, c'est ce que j'ai fait pour les couleurs.

**Avantages et inconvénients ici :** Le double dispatch est bien quand les objets sont de vraies classes différentes, comme les pièces, mais ici il ferait beaucoup de classes et de méthodes pour rien. La table est plus simple pour des valeurs comme les couleurs. J'ai donc gardé le dispatch sur la classe des pièces et utilisé des tables pour les couleurs.

## Solutions écartées

- **Pattern State** pour la prise en passant : pas adapté ici, car l’échiquier ne change pas de comportement, il doit juste se souvenir du dernier pion qui a avancé de deux cases. Le Null Object suffit pour éviter le nil
- **Prise en passant sans Null Object** (avec une simple collection) : plus courte, mais moins claire, j'ai gardé le Null Object.
- **Double dispatch complet sur les couleurs** : il aurait fallu créer des classes pour chaque couleur de pièce et de case, avec environ une vingtaine de méthodes.
- **Supprimer tous les `if` à tout prix**, j'ai gardé le `ifFalse:` de `moveTo:` , parce que le remplacer aurait rendu le code moins lisible.

## Suite

- Finir le kata 2 : écrire une seule méthode `renderPieceOn:` dans `MyPiece`, qui demande à la case d'écrire la lettre de la pièce, puis supprimer les `renderPieceOn:` de chaque pièce et les six méthodes `renderPawn:`, `renderKing:`, etc.. de `MyChessSquare`. Les tests de `MyPieceRenderingTest` doivent rester verts. Il restera aussi le `if` des cases vides (`z` ou `x`), que je pourrai traiter de la même façon.
- Corriger le bug du jeu lancé depuis le Playground, le pion n'y est pas promu, parce que l'interface ne propose pas de choix, alors que tous les tests sont verts.
- Chercher d'autres design patterns pour refactorer le code, par exemple un Null Object pour les cases vides (qui contiennent encore nil) ou Strategy pour les bots et le choix de promotion.
- Faire d'autres katas si possible, comme *Remove nil checks* ou *Add pawn promotion* en continuité avec le bug que j'ai cité juste au dessus.
