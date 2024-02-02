# Singleton

## Design pattern de manière globale :
L'objectif est de restreindre l'instanciation d'une classe à un seul objet.

## Avantages :
Permet de garantir qu'une classe ne possède qu'une seule instance, tout en fournissant un point d'accès global à cette instance.

## Inconvénients : 
+ Code supplémentaire et pas forcément explicite

## Représentation UML : 
![Alt text](https://media.discordapp.net/attachments/884824217110061117/1195359425448390697/image.png?ex=65b3b437&is=65a13f37&hm=2d6c59e1667f772efb86d49f8965678bc078030458c8752a9752e93f0c523ea3&=&format=webp&quality=lossless)

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
Ce script php retourne : 
![Alt text](https://media.discordapp.net/attachments/884824217110061117/1202931434784956516/image.png?ex=65cf4033&is=65bccb33&hm=511d9b7f9671ee122b901671412f9a2b35e1527dd34109a3b9871bebade00491&=&format=webp&quality=lossless)
