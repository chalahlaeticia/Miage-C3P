## Hammed ABASS

Cette semaine, j'ai continué le jeu d'échecs pour mettre en pratique les notions du cours.

J'ai travaillé sur la différence entre délégation et héritage. Le joueur utilise maintenant un autre objet pour choisir son prochain déplacement, au lieu de faire ce choix directement. Ça permet de changer sa façon de jouer sans créer une nouvelle sous-classe de joueur.

J'ai aussi utilisé un Visitor pour compter les pièces sur le plateau, une Command pour représenter un déplacement avant de l'exécuter, et un Decorator pour garder une trace des déplacements proposés par une stratégie. Avec ces exemples dans le projet, je comprends mieux à quoi ces patterns peuvent servir.

J'ai ensuite regardé `MySelectedState` et `MyUnselectedState` pour comprendre comment les clics sont gérés. J'ai repéré un problème : si je sélectionne une pièce puis que le bouton Play la déplace, les anciennes cases possibles peuvent rester surlignées après le clic suivant. J'ai trouvé d'où vient le problème, mais je ne l'ai pas encore corrigé.

Je me repère mieux dans le code et j'arrive à faire plus facilement le lien entre les exemples du cours et le projet.

[Mon dépôt ChessPharo](https://github.com/AbassHammed/ChessPharo)

## Julie LIM

Cette semaine, j'ai continué à tester le projet Chess et à corriger plusieurs problèmes liés aux déplacements manuels

J'ai d'abord corrigé le problème où un clic sur une case non valide pouvait être considéré comme un déplacement
Cela pouvait provoquer un changement de joueur même si aucune pièce n'avait réellement bougé

Pour le corriger j'ai ajouté une vérification afin de m'assurer que la case sélectionnée fait bien partie des déplacements autorisés de la pièce avant d'effectuer le mouvement et de passer au joueur suivant

J'ai également commencé à regarder le fonctionnement de l'échec et mat
La méthode checkForMate existe déjà dans le projet, mais son exécution provoque une erreur
J'ai donc commencé à suivre les différentes méthodes appelées (isCheckMated, opponentPieces, board) afin d'identifier l'origine du problème

Je n'ai cependant pas encore trouvé la solution pour le échec et mat
