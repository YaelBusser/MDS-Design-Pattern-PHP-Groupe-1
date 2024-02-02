# Design Pattern Memento

## Définition

Le Memento est un patron de conception comportemental qui permet de capturer et de restaurer l'état interne d'un objet
sans révéler les détails de son implémentation. Il est très utilisé pour les éditeur de texte quand il s'agit de
retourner la valeur du texte à un état antérieur.

## Avantages

### 1. Préservation de l'encapsulation

Le Memento permet de sauvegarder et de restaurer l'état d'un objet sans violer l'encapsulation. L'objet d'origine peut
rester fermé aux autres objets, car seule la classe Memento connaît les détails de l'état sauvegardé.

### 2. Possibilité de revenir à un état antérieur

Le Memento offre la possibilité de revenir à un état antérieur d'un objet. Cela peut être utile dans des scénarios tels
que l'annulation d'opérations.

### 3. Simplification du code

En utilisant le Memento, le code peut être simplifié, car il n'a pas besoin de connaître les détails internes de
l'objet pour effectuer des opérations de sauvegarde et de restauration.

## Inconvénients

### 1. Coût en termes de performances et de mémoire

Sauvegarder et restaurer l'état d'un objet peut avoir un coût en termes de performances et de mémoire, surtout si
l'objet a un état complexe.

### 2. Gestion des versions

La gestion des versions des objets peut devenir complexe si de nombreux états sont sauvegardés. Cela peut entraîner une
consommation excessive de mémoire et une complexité accrue dans la gestion des différents états.

## Représentation UML

Le Memento permet de capturer et de restaurer l'état interne d'un objet.
Nous allons prendre l'exemple d'un éditeur de texte où l'utilisateur écrit une phrase puis il fait un controle+z afin de
revenir à l'avant dernière sauvegarde du texte mais il supprime avant la dernière sauvegarde du texte.
Ce qui fait donc que l'avant dernière sauvegarde du texte devient la dernière sauvegarde.
Voici un exemple de structure UML de cet exemple.
![UML Memento](https://i.ibb.co/nR38k44/UML-momento.png)

## Implémentation en PHP

```php
<?php

// Memento
class TextEditorMemento
{
    private $content;

    public function __construct($content)
    {
        $this->content = $content;
    }

    public function getContent()
    {
        return $this->content;
    }
}

// Originator
class TextEditor
{
    private $content;
    private $history;

    public function __construct()
    {
        $this->history = new History();
    }

    public function write($text)
    {
        $this->content .= $text;
    }

    public function getContent()
    {
        return $this->content;
    }

    public function save()
    {
        $this->history->addMemento(new TextEditorMemento($this->content));
    }

    public function undo()
    {
        $lastMemento = $this->history->getPreviousMemento();
        if ($lastMemento !== null) {
            $this->content = $lastMemento->getContent();
        }
    }
}

// Caretaker
class History
{
    private $mementos = [];

    public function addMemento(TextEditorMemento $memento)
    {
        $this->mementos[] = $memento;
    }

    public function getPreviousMemento()
    {
        if (count($this->mementos) > 1) {
            array_pop($this->mementos);
            return end($this->mementos);
        }

        return null;
    }
}

$textEditor = new TextEditor();

$textEditor->write("CS ");
$textEditor->save();

$textEditor->write("< ");
$textEditor->save();

$textEditor->write("Valorant");
echo "Texte actuel : " . $textEditor->getContent() . "\n";

// L'utilisateur fait 2 ctrl+z
$textEditor->undo();
$textEditor->undo();
echo "Texte après 2 control+z : " . $textEditor->getContent() . "\n";

$textEditor->write("> ");
$textEditor->save();

$textEditor->write("Valorant");
$textEditor->save();

echo "Texte actuel mit à jour : " . $textEditor->getContent() . "\n";
```
Ce script php retourne : ![return memento script php](https://i.ibb.co/r2sXb4n/return-memento.png)