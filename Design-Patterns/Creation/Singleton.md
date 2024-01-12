# Singleton

## Design pattern de manière globale :
L'objectif est de restreindre l'instanciation d'une classe à un seul objet.

## Avantages :
Permet de garantir qu'une classe ne possède qu'une seule instance, tout en fournissant un point d'accès global à cette instance.

## Inconvénients : 
+ code, pas forcément explicite

## Représentation UML : 
![Alt text]([https://www.tutorialspoint.com/design_pattern/images/singleton_pattern_uml_diagram.jpg](https://discord.com/channels/@me/884824217110061117/1195359425725206578) "a title")

## Implémentation en PHP :

``` php
<?php

class Singleton
{

    private static $instance = [];

    public static function getInstance(): Singleton
    {
        $cls = static::class;
        if (!isset(self::$instance[$cls])) {
            self::$instance[$cls] = new static();
        }

        return self::$instance[$cls];
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
