# Fabrique(Factory Method)

## Design pattern de manière globale :
Fabrique est un patron de conception de création qui définit une interface pour créer des objets dans une classe mère, mais délègue le choix des types d’objets à créer aux sous-classes.
Donc permet de déléguer la responsabilité de l'instanciation des objets à des sous-classes, offrant ainsi une flexibilité dans la création d'objets.

## Avantages :
- Délègue la création d'objets aux sous-classes, permettant une extension facile.
- Favorise la cohérence entre les produits créés par différentes sous-classes.

## Inconvénients : 
- Peut entraîner la création d'un grand nombre de classes si de nombreux produits et variantes sont présents.

Par exemple :
## Représentation UML : 
![Alt text](https://refactoring.guru/images/patterns/diagrams/factory-method/solution1.png)

ou pour correspondre à mon code :
![UmlCorrespondCode](https://media.discordapp.net/attachments/884824217110061117/1202904927186194452/image.png?ex=65cf2783&is=65bcb283&hm=4c1a37d4517a0307cb2ff64fede67bd947b7eb1b643041f9ef6c0e70359e6147&=&format=webp&quality=lossless&width=252&height=670)

## Implémentation en PHP :
``` php
<?php

// Produit Abstrait
interface Meuble {
    public function afficher(): void;
}

// Produit Concret
class ChaiseModerne implements Meuble {
    public function afficher(): void {
        echo "Chaise Moderne\n";
    }
}

// Interface de Fabrique (Factory Method)
interface FabriqueMeubles {
    public function creerMeuble(): Meuble;
}

// Fabrique Concrète
class FabriqueModerne implements FabriqueMeubles {
    public function creerMeuble(): Meuble {
        return new ChaiseModerne();
    }
}

// Client
function utiliserMeuble(FabriqueMeubles $fabrique): void {
    $meuble = $fabrique->creerMeuble();

    echo "Utilisation d'un meuble :\n";
    $meuble->afficher();
}

// Simulation
echo "Utilisation d'un meuble moderne :\n";
utiliserMeuble(new FabriqueModerne());
```
