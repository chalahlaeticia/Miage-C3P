# Rapport hebdomadaire semaine 4

### Ce que j'ai fait
J'ai lu toutes les slides du Lect05 - Coupling (M9-1, M4-5, M3-5, M9-5). J'ai révisé ce que j'ai appris la semaine dernière. J'ai commencé à essayer de m'approprier le code du projet des échecs pour ensuite pouvoir le modifier. Je préfère essayer de comprendre le fonctionnement de tout le code et du système pour ne pas modifier n'importe quoi et juste faire des patchs "pensements".

### Ce que j'ai appris
- Il vaut mieux éviter de stocker les singletons dans des variables globales car les classes des singletons agissent déjà comme des portes d'accès globables.
- En Pharo il existe deux types de variables partagées (équivalent des attributs statiques en Java selon moi, si j'ai bien compris) : celles partagées dans la classe même et toutes les classes qui héritent de celles ci (Shared Variable) et celles partagées seulement dans la même classe (Class Instance Variable)
- En Pharo, Transcript est une variable globale qui pointe vers une instance de stream qui sert à log
- Si possible, éviter les singletons, éviter les variables globales => rend le code moins modulaire, moins testable