# Singleton

## Design pattern de manière globale :
L'objectif est de restreindre l'instanciation d'une classe à un seul objet.

## Avantages :
Permet de garantir qu'une classe ne possède qu'une seule instance, tout en fournissant un point d'accès global à cette instance.

## Inconvénients : 
+ code, pas forcément explicite

## Représentation UML : 
![Alt text](https://www.tutorialspoint.com/design_pattern/images/singleton_pattern_uml_diagram.jpg "a title")

## Implémentation en PHP :

``` php
<?php

class Singleton
{

    private static $instances = [];

    public static function getInstance(): Singleton
    {
        $cls = static::class;
        if (!isset(self::$instances[$cls])) {
            self::$instances[$cls] = new static();
        }

        return self::$instances[$cls];
    }

}

$s1 = Singleton::getInstance();
$s2 = Singleton::getInstance();
if ($s1 === $s2) {
    echo "Le singleton a fonctionné ! ça a fait une instance";
} else {
    echo "Singleton non fonctionnel.";
}
```
