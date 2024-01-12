# Monteur(Builder)

## Design pattern de manière globale :
Utilisé pour construire un objet complexe étape par étape. Il permet de créer différentes représentations d'un objet en utilisant le même processus de construction.
Par exemple la construction d'un ordinateur étape par étape.

## Avantages :
Permet la construction d'objets complexes de manière étape par étape.
Isole le processus de construction de la représentation finale de l'objet.
Facilite la création de plusieurs variantes d'un même objet.

## Inconvénients : 
Peut introduire une complexité supplémentaire dans le code.
Nécessite la mise en place d'une interface ou d'une classe abstraite pour le constructeur.

## Représentation UML : 
![Alt text](https://media.discordapp.net/attachments/884824217110061117/1195359425448390697/image.png?ex=65b3b437&is=65a13f37&hm=2d6c59e1667f772efb86d49f8965678bc078030458c8752a9752e93f0c523ea3&=&format=webp&quality=lossless)

## Implémentation en PHP :
``` php
<?php

// Produit : Ordinateur
class Ordinateur
{
    public $type;
    public $processeur;
    public $memoire;
    public $stockage;

    public function spécifications()
    {
        echo "Type: {$this->type}, Processeur: {$this->processeur}, Mémoire: {$this->memoire}, Stockage: {$this->stockage}\n";
    }
}

// Constructeur abstrait : Constructeur d'Ordinateur
interface ConstructeurOrdi
{
    public function construireProcesseur();
    public function construireMemoire();
    public function construireStockage();
    public function getResult(): Ordinateur;
}

// Constructeur concret : Constructeur d'Ordinateur 
class ConstructeurOrdinateur implements ConstructeurOrdi
{
    private $ordinateur;

    public function __construct()
    {
        $this->ordinateur = new Ordinateur();
        $this->ordinateur->type = "Ordinateur fixe";
    }

    public function construireProcesseur()
    {
        $this->ordinateur->processeur = "Intel Core i5";
    }

    public function construireMemoire()
    {
        $this->ordinateur->memoire = "8 Go";
    }

    public function construireStockage()
    {
        $this->ordinateur->stockage = "256 Go SSD";
    }

    public function getResult(): Ordinateur
    {
        return $this->ordinateur;
    }
}

// Utilisation
$constructeur = new ConstructeurOrdinateur();
$constructeur->construireProcesseur();
$constructeur->construireMemoire();
$constructeur->construireStockage();
$ordinateur = $constructeur->getResult();

echo "Ordinateur :\n";
$ordinateur->spécifications();
```
