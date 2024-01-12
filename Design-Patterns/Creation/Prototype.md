# Prototype(Clone)

## Design pattern de manière globale :
Permet de créer de nouveaux objets en copiant un objet existant, appelé prototype. 
Évite de créer une classe spécifique pour chaque type d'objet à instancier, en utilisant un mécanisme de clonage.

## Avantages :
Facilite la création de nouveaux objets en clonant des prototypes existants.
Permet d'ajouter ou de supprimer des fonctionnalités dynamiquement.
Réduit la nécessité de sous-classes.

## Inconvénients : 
La définition des classes et des prototypes peut devenir complexe.
Les objets clonés peuvent nécessiter une initialisation supplémentaire.

## Représentation UML : 
![Alt text](https://media.discordapp.net/attachments/884824217110061117/1195367846037958767/image.png?ex=65b3bc0f&is=65a1470f&hm=395968b6c8e6b377a157a3e77bc3604f84cd7e06971f303a76b738e3ac7e357c&=&format=webp&quality=lossless)

## Implémentation en PHP :
``` php
<?php

class Prototype
{
    private $name;

    public function __construct($name)
    {
        $this->name = $name;
    }

    public function duplicate()
    {
        return new self($this->name);
    }

    public function getName()
    {
        return $this->name;
    }
}

// Usage
$prototype = new Prototype('Prototype Object');
$clone = $prototype->duplicate();

echo $prototype->getName()."\n";
echo $clone->getName(); 
```
