# Design Pattern État (State)

## Définition

Le design pattern État est un patron de conception comportemental qui permet à un objet de modifier son comportement
lorsqu'il change son état interne. Il permet à l'objet de paraître modifié à l'extérieur sans changer sa classe.

## Avantages

### 1. Encapsulation de l'état

L'état d'un objet est encapsulé dans des classes distinctes, ce qui facilite la gestion et la maintenance du code.

### 2. Simplification des transitions d'état

Le pattern État simplifie les transitions d'état en les modélisant sous forme de classes, évitant ainsi une multitude de
conditions.

### 3. Facilité d'ajout de nouveaux états

L'ajout de nouveaux états se fait facilement en introduisant de nouvelles classes sans modifier les classes existantes.

## Inconvénients

### 1. Nombre élevé de classes

Le pattern État peut entraîner un grand nombre de classes, en particulier lorsque l'objet a de nombreux états et
transitions.

### 2. Complexité accrue

La complexité du code peut augmenter, surtout si le nombre d'états et de transitions est important.

## Représentation UML

Le pattern État utilise différentes classes pour représenter les différents états d'un objet et définit une interface
commune pour les comportements associés à ces états.

Nous allons prendre l'exemple suivant : On utilise une lampe pour représenter le contexte, avec deux états possibles :
allumé (OnState) et éteint (
OffState). La lampe peut être allumée ou éteinte, et les actions (turnOn et turnOff) modifient l'état de la lampe en
conséquence.

Voici un exemple de structure UML de cet exemple.

![UML State](https://i.ibb.co/MZNK9Dj/UML-state.png)

## Implémentation en PHP

```php
<?php

interface State
{
    public function turnOn();
    public function turnOff();
}

class OnState implements State
{
    public function turnOn()
    {
        echo "La lampe est déjà allumée.\n";
        return $this;
    }

    public function turnOff()
    {
        echo "La lampe est éteinte maintenant.\n";
        return new OffState();
    }
}

class OffState implements State
{
    public function turnOn()
    {
        echo "La lampe est allumée maintenant.\n";
        return new OnState();
    }

    public function turnOff()
    {
        echo "La lampe est déjà éteinte.\n";
        return $this;
    }
}

class Lamp
{
    private $state;

    public function __construct()
    {
        $this->state = new OffState();
    }

    public function turnOn()
    {
        $this->state = $this->state->turnOn();
    }

    public function turnOff()
    {
        $this->state = $this->state->turnOff();
    }
}

$lamp = new Lamp();

$lamp->turnOff();
$lamp->turnOn();
$lamp->turnOff();
$lamp->turnOff();
$lamp->turnOn();
$lamp->turnOn();
```

Ce script php retourne :

![return state script php](https://i.ibb.co/phGSrcC/return-state.png)