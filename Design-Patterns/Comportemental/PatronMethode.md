# Patron de méthode (Méthode socle, Template Method)

## Design pattern de manière globale :
Le Patron de Méthode définit le squelette d'un algorithme dans une méthode, mais laisse certaines étapes aux sous-classes. 
Donc, les sous-classes peuvent redéfinir certaines étapes de l'algorithme sans changer sa structure globale.

## Avantages :
- Favorise la réutilisation du code en fournissant une structure commune dans la méthode principale.
- Permet de définir des étapes spécifiques dans les sous-classes tout en maintenant la cohérence globale de l'algorithme.
- Facilite l'extension de certaines parties de l'algorithme sans altérer les autres parties.

## Inconvénients : 
- Peut rendre le code plus difficile à comprendre si les sous-classes modifient fréquemment le comportement de l'algorithme.
- L'implémentation par défaut de certaines étapes peut limiter la flexibilité de l'algorithme.

## Représentation UML : 
![Alt text]()

## Implémentation en PHP :
``` php

```
