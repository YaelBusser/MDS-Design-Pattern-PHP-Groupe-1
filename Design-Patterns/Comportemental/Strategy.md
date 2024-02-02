# Design Pattern Strategy

## Définition

Le design pattern Strategy est un patron de conception comportemental qui permet de définir une famille d'algorithmes,
encapsuler chacun d'eux, et les rendre interchangeables. Il permet à un client de choisir l'algorithme approprié à
utiliser à partir d'une famille d'algorithmes, indépendamment des clients qui les utilisent.

## Avantages

### 1. Encapsulation des algorithmes

Le pattern Strategy permet d'encapsuler chaque algorithme dans une classe distincte, facilitant ainsi la gestion,
l'extension, et la réutilisation du code.

### 2. Interchangeabilité des algorithmes

Les algorithmes peuvent être facilement interchangeables, ce qui permet de changer le comportement d'un objet contexte
sans modifier sa structure.

### 3. Facilité de test

Chaque algorithme encapsulé peut être testé de manière indépendante, facilitant le processus de test et de débogage.

### 4. Réduction du couplage

Le couplage entre le client et les algorithmes est réduit, car le client n'a pas besoin de connaître les détails de
chaque algorithme. Cela favorise une architecture plus souple et évolutive.

## Inconvénients

### 1. Complexité accrue

L'ajout de nombreuses classes peut augmenter la complexité globale du code, surtout pour des situations simples où une
seule stratégie suffirait.

### 2. Configuration nécessaire

Le client doit être configuré avec la bonne stratégie, ce qui peut rendre l'initialisation complexe.

### 3. Taille du code

L'utilisation du pattern Strategy peut entraîner une augmentation de la taille du code en raison de la multiplication
des classes.

## Représentation UML

Nous allons prendre l'exemple suivant : On utilise une lampe pour représenter le contexte, avec deux états possibles :
allumé (OnState) et éteint (
OffState). La lampe peut être allumée ou éteinte, et les actions (turnOn et turnOff) modifient l'état de la lampe en
conséquence.

Voici un exemple de structure UML de cet exemple.

![UML Strategy](https://i.ibb.co/zhKZ5Sn/UML-strategy.png)

## Implémentation en PHP

```php
<?php

interface TransportStrategy
{
    public function goToAirport();
}

class BusTransport implements TransportStrategy
{
    public function goToAirport()
    {
        echo "Prendre le bus pour se rendre à l'aéroport.\n";
    }
}

class TaxiTransport implements TransportStrategy
{
    public function goToAirport()
    {
        echo "Commander un taxi pour se rendre à l'aéroport.\n";
    }
}

class BikeTransport implements TransportStrategy
{
    public function goToAirport()
    {
        echo "Monter à vélo pour se rendre à l'aéroport.\n";
    }
}

class Traveler
{
    private $transportStrategy;

    public function setTransportStrategy(TransportStrategy $transportStrategy)
    {
        $this->transportStrategy = $transportStrategy;
    }

    public function travelToAirport()
    {
        $this->transportStrategy->goToAirport();
    }
}

$traveler = new Traveler();

$traveler->setTransportStrategy(new BusTransport());
$traveler->travelToAirport();

$traveler->setTransportStrategy(new TaxiTransport());
$traveler->travelToAirport();

$traveler->setTransportStrategy(new BikeTransport());
$traveler->travelToAirport();
```

Ce script php retourne :

![return strategy script php](https://i.ibb.co/yNfnzYk/return-strategy.png)