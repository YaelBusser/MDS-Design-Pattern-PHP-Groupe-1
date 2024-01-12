# Design Pattern Médiateur (Mediator)

## Design pattern de manière globale

Le Médiateur est un patron de conception comportemental qui diminue le couplage entre les composants d’un programme, en
les faisant communiquer indirectement, via un objet médiateur spécial.

## Avantages

### 1. Réduction des dépendances directes

Le médiateur réduit les dépendances directes entre les composants d'un système. Chaque composant communique uniquement
avec le médiateur, ce qui facilite la maintenance et la modification du système.

### 2. Centralisation de la logique de coordination

La logique de coordination est centralisée dans le médiateur. Cela peut rendre le système plus facile à
comprendre et à gérer, car la coordination n'est pas dispersée entre plusieurs composants.

### 3. Facilitation des échanges entre composants

Le médiateur facilite les échanges entre les composants en fournissant un point centralisé pour gérer les
communications. Cela peut rendre la communication entre composants plus efficace.

### 4. Encapsulation du comportement collectif

Le médiateur encapsule le comportement collectif des composants. Cela signifie que les composants individuels
n'ont pas besoin de connaître les détails internes des autres composants, ce qui renforce l'encapsulation.

## Inconvénients

### 1. Complexité potentielle

Dans des systèmes complexes, la logique de coordination peut devenir complexe, en particulier si de nombreux composants
sont impliqués. Cela peut rendre la compréhension du système plus difficile.

### 2. Perte de l'isolation des composants

Si la médiation n'est pas bien gérée, le médiateur peut devenir un point de connexion centralisé critique. Les
changements dans le médiateur peuvent avoir un impact sur l'ensemble du système.

### 3. Difficulté à introduire de nouveaux composants

Introduire de nouveaux composants peut être plus complexe, car cela peut nécessiter des modifications dans le médiateur
pour gérer les nouvelles interactions.

### 4. Potentiel pour devenir surchargé

Si le médiateur gère trop de responsabilités, il peut devenir surchargé et violer le principe de responsabilité unique.

## Représentation UML

Le médiateur permet aux utilisateurs de communiquer entre eux sans avoir à connaître les détails de l'implémentation des
autres utilisateurs. Le médiateur facilite cette communication en centralisant la coordination et en réduisant les
dépendances directes entre les utilisateurs.

Voici un exemple avec un utilisateur qui envoit un message à d'autres utilisateurs.
![UML Médiateur](https://i.ibb.co/st55t4q/Capture-d-cran-2024-01-12-163627.png)

## Implémentation en PHP

```php
<?php

interface Mediator
{
    public function sendMessage(User $user, $message);
}

class ConcreteMediator implements Mediator
{
    private $users = [];

    public function addUser(User $user)
    {
        $this->users[] = $user;
    }

    public function sendMessage(User $user, $message)
    {
        foreach ($this->users as $recipient) {
            if ($recipient !== $user) {
                $recipient->receiveMessage($user, $message);
            }
        }
    }
}

class User
{
    private $name;
    private $mediator;

    public function __construct($name)
    {
        $this->name = $name;
    }

    public function setMediator(Mediator $mediator)
    {
        $this->mediator = $mediator;
    }

    public function getName()
    {
        return $this->name;
    }

    public function sendMessage($message)
    {
        $this->mediator->sendMessage($this, $message);
    }

    public function receiveMessage(User $sender, $message)
    {
        echo $this->name . " a reçu de " . $sender->getName() . " : " . $message . "\n";
    }
}

$yael = new User("Yael");
$adrien = new User("Adrien");
$timeo = new User("Timéo");

$mediator = new ConcreteMediator();

$mediator->addUser($yael);
$mediator->addUser($adrien);
$mediator->addUser($timeo);

$yael->setMediator($mediator);

$yael->sendMessage("Salut");
```
