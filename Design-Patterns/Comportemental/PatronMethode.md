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
![Alt text](https://media.discordapp.net/attachments/884824217110061117/1202927177599946773/image.png?ex=65cf3c3c&is=65bcc73c&hm=38bf29938defaf4bfdb89522409320b7b940ea2924ad0d181f04fc522ba49633&=&format=webp&quality=lossless)

## Implémentation en PHP :
``` php
<?php

// Classe abstraite avec le patron de méthode
abstract class Algorithme {
    // Le Patron de Méthode (Template Method)
    public function execute(): void {
        $this->etape1();

        $this->etape2();

        $this->etape3();
    }

    protected abstract function etape1(): void;

    protected function etape2(): void {
        // Par défaut, une implémentation générique
        echo "Implémentation générique de l'étape 2\n";
    }

    protected abstract function etape3(): void;
}

// Implémentation concrète
class AlgorithmeConcret extends Algorithme {
    // Redéfinition de l'étape 1 pour une implémentation spécifique
    protected function etape1(): void {
        echo "Implémentation spécifique de l'étape 1\n";
    }

    // Étape 2 reste inchangée, utilisant l'implémentation générique de la classe mère

    // Redéfinition de l'étape 3 pour une implémentation spécifique
    protected function etape3(): void {
        echo "Implémentation spécifique de l'étape 3\n";
    }
}

// Client
function utiliserAlgorithme(Algorithme $algorithme): void {
    echo "Utilisation de l'algorithme :\n";
    $algorithme->execute();
}

// Simulation
utiliserAlgorithme(new AlgorithmeConcret());
```
