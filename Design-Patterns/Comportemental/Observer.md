# Design Pattern Observer

## Définition

Le design pattern Observer est un patron de conception comportemental qui définit une dépendance entre objets de manière
à ce
que lorsqu'un objet change d'état, tous ses dépendants en soient notifiés et mis à jour automatiquement. Cela permet
d'établir un couplage lâche entre les sujets (objets qui changent d'état) et les observateurs (objets qui réagissent à
ces changements).

## Avantages

### 1. Couplage lâche

Le pattern Observer réduit le couplage entre les objets, car les sujets n'ont pas besoin de connaître les détails de
leurs observateurs. Ils communiquent simplement via des interfaces.

### 2. Modularité et réutilisabilité

Les observateurs peuvent être ajoutés ou supprimés facilement sans affecter le sujet, ce qui favorise la modularité et
la réutilisabilité du code.

### 3. Notifications automatiques

Lorsqu'un sujet change d'état, tous les observateurs sont automatiquement notifiés, ce qui simplifie la gestion des
mises à jour.

## Inconvénients

### 1. Complexité accrue

L'utilisation excessive d'observateurs peut rendre le code complexe à comprendre, en particulier lorsque plusieurs
objets sont impliqués.

### 2. Risque de fuites mémoire

Si la gestion des références n'est pas correctement gérée, il peut y avoir des risques de fuites mémoire, surtout si des
observateurs ne sont pas correctement détachés.

## Représentation UML

Considérons un exemple où nous avons un sujet qui représente un blog et des observateurs qui
représentent les abonnés à ce blog. Chaque fois qu'un nouvel article est publié, tous les abonnés sont notifiés.
Voici un exemple de structure UML de cet exemple.

![UML Observer](https://i.ibb.co/TB66b8x/UML-observer.png)

## Implémentation en PHP
```php
<?php

class BlogPost extends BlogSubscriber
{
    private $title;
    private $content;
    private $observers = [];

    public function attach(Observer $observer)
    {
        $this->observers[] = $observer;
    }

    public function publishPost($title, $content)
    {
        $this->title = $title;
        $this->content = $content;
        $this->notifyObservers();
    }

    private function notifyObservers()
    {
        foreach ($this->observers as $observer) {
            $observer->update($this);
        }
    }

    public function getTitle()
    {
        return $this->title;
    }

    public function getContent()
    {
        return $this->content;
    }
}

interface Observer
{
    public function update(BlogPost $blogPost);
}

class BlogSubscriber implements Observer
{
    private $name;

    public function __construct($name)
    {
        $this->name = $name;
    }

    public function update(BlogPost $blogPost)
    {
        echo "Salut {$this->name}, un nouveau sujet a été publié !\n";
        echo "Titre: {$blogPost->getTitle()}\n";
        echo "Contenu: {$blogPost->getContent()}\n\n";
    }
}

$blog = new BlogPost();

$subscriber1 = new BlogSubscriber("Adrien");
$subscriber2 = new BlogSubscriber("Timéo");
$subscriber3 = new BlogSubscriber("Martin");

$blog->attach($subscriber1);
$blog->attach($subscriber2);

$blog->publishPost("Pourquoi CS est mieux que Valorant ?", "-Valorant a été inspiré par CS \n -CS a un meilleur contrôle. \n -CS a plus de défi. \n -Il est plus difficile de distinguer les personnages sur CS");

```

Ce script php retourne : 

![return observer script php](https://i.ibb.co/ZMbJjJv/return-observer.png)