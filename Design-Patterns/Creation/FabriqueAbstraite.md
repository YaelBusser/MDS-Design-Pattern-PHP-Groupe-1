# Fabrique Abstraite (Abstract Factory)

## Design pattern de manière globale :
Utilisé pour créer des familles d'objets liés ou inter-dépendants sans avoir à préciser au moment de leur création la classe concrète à utiliser.
Cela permet de rendre un système indépendant de la manière dont ses objets sont créés, composés et représentés.

## Avantages :
- Abstraction des détails de création : La fabrique abstraite permet de créer des familles d'objets sans se soucier des détails concrets de leur création, favorisant ainsi une plus grande modularité du code.

- Garantit la cohérence : En utilisant une fabrique abstraite, on s'assure que les objets créés appartiennent à la même famille, garantissant ainsi une cohérence dans le système.

- Facilite l'ajout de nouvelles familles d'objets : L'ajout de nouvelles familles d'objets se fait simplement en introduisant de nouvelles classes de fabriques, sans avoir à modifier le code existant.

## Inconvénients : 
- Complexité accrue : Introduire une fabrique abstraite peut rendre le code plus complexe, notamment si le nombre de familles d'objets est limité et ne change pas fréquemment.

- Extension complexe : Ajouter de nouveaux types d'objets peut nécessiter l'extension de l'interface de la fabrique abstraite, ce qui peut entraîner des modifications dans plusieurs parties du code.

## Représentation UML : 
![Alt text](https://media.discordapp.net/attachments/884824217110061117/1202893928093974558/image.png?ex=65cf1d45&is=65bca845&hm=e63933a6d10287988c5601ab13479d64d65f4f05fce3fccdeb055e120be576d8&=&format=webp&quality=lossless&width=720&height=670)
ou
![Alt text](https://refactoring.guru/images/patterns/diagrams/abstract-factory/solution2.png?id=53975d6e4714c6f942633a879f7ac571)

Exemple que j'ai pris et simplifié à partir de : ![Alt text](https://refactoring.guru/fr/design-patterns/abstract-factory). Il utilise le design pattern de Fabrique Abstraite pour créer des produits sans spécifier les détails concrets, facilitant ainsi l'ajout de nouveaux styles.
## Implémentation en PHP :

``` php
<?php

// Produit Abstrait
interface Meuble {
    public function afficher(): void;
}

// Produits Concrets
class ChaiseModerne implements Meuble {
    public function afficher(): void {
        echo "Chaise Moderne\n";
    }
}

class CanapeModerne implements Meuble {
    public function afficher(): void {
        echo "Canapé Moderne\n";
    }
}

class ChaiseVictorienne implements Meuble {
    public function afficher(): void {
        echo "Chaise Victorienne\n";
    }
}

class CanapeVictorien implements Meuble {
    public function afficher(): void {
        echo "Canapé Victorien\n";
    }
}

class ChaiseArtDeco implements Meuble {
    public function afficher(): void {
        echo "Chaise Art Déco\n";
    }
}

class CanapeArtDeco implements Meuble {
    public function afficher(): void {
        echo "Canapé Art Déco\n";
    }
}

// Fabrique Abstraite
interface FabriqueMeubles {
    public function creerChaise(): Meuble;
    public function creerCanape(): Meuble;
}

// Fabriques Concrètes
class FabriqueModerne implements FabriqueMeubles {
    public function creerChaise(): Meuble {
        return new ChaiseModerne();
    }

    public function creerCanape(): Meuble {
        return new CanapeModerne();
    }
}

class FabriqueVictorienne implements FabriqueMeubles {
    public function creerChaise(): Meuble {
        return new ChaiseVictorienne();
    }

    public function creerCanape(): Meuble {
        return new CanapeVictorien();
    }
}

class FabriqueArtDeco implements FabriqueMeubles {
    public function creerChaise(): Meuble {
        return new ChaiseArtDeco();
    }

    public function creerCanape(): Meuble {
        return new CanapeArtDeco();
    }
}

// Client
function creerEnsembleMeubles(FabriqueMeubles $fabrique): void {
    $chaise = $fabrique->creerChaise();
    $canape = $fabrique->creerCanape();

    echo "Ensemble de meubles créé avec :\n";
    $chaise->afficher();
    $canape->afficher();
}

// Simulation
echo "Création d'un ensemble de meubles modernes :\n";
creerEnsembleMeubles(new FabriqueModerne());

echo "\nCréation d'un ensemble de meubles victoriens :\n";
creerEnsembleMeubles(new FabriqueVictorienne());

echo "\nCréation d'un ensemble de meubles Art Déco :\n";
creerEnsembleMeubles(new FabriqueArtDeco());
```
