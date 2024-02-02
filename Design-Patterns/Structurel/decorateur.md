# Décorateur (Decorator)

## Design pattern de manière globale :
Le Décorateur est un design pattern structurel qui permet d'ajouter dynamiquement des fonctionnalités supplémentaires à un objet sans modifier sa structure interne. Ce modèle est utile pour étendre les capacités d'un objet de manière flexible et réutilisable, en enveloppant l'objet dans une classe décorateur qui ajoute les nouvelles fonctionnalités.

## Avantages :
1. **Flexibilité** : Permet d'ajouter ou de retirer des fonctionnalités à un objet à l'exécution sans altérer les objets existants.
2. **Extension** : Favorise l'extension des fonctionnalités d'un objet sans hériter de celui-ci, respectant ainsi le principe d'ouverture/fermeture.
3. **Composition sur l'héritage** : Utilise la composition à la place de l'héritage, offrant une approche plus flexible pour étendre les fonctionnalités.

## Inconvénients :
1. **Complexité** : Peut introduire une complexité supplémentaire et rendre le code plus difficile à comprendre à cause des multiples couches.
2. **Surcharge** : L'utilisation excessive de décorateurs peut entraîner une surcharge de performance due à la profondeur accrue de la pile d'appels.

## Représentation UML :
![Image](https://cdn.discordapp.com/attachments/884824217110061117/1202932327030988880/image.png?ex=65cf4108&is=65bccc08&hm=fd6368a11a97bd6c6c20ab562133fad5594c635166cf6c8d7156d71dc4d80e91&)

## Implémentation en PHP :
```php
<?php

// Component Interface
interface Component {
    public function operation(): string;
}

// ConcreteComponent
class ConcreteComponent implements Component {
    public function operation(): string {
        return "ConcreteComponent";
    }
}

// Decorator Abstract Class
abstract class Decorator implements Component {
    protected $component;

    public function __construct(Component $component) {
        $this->component = $component;
    }

    public function operation(): string {
        return $this->component->operation();
    }
}

// ConcreteDecorator
class ConcreteDecorator extends Decorator {
    public function operation(): string {
        // Appel de l'opération du composant, puis extension de son comportement
        return "ConcreteDecorator(" . parent::operation() . ")";
    }
}

// Utilisation du Décorateur
$component = new ConcreteComponent();
$decorator = new ConcreteDecorator($component);
echo $decorator->operation();

?>
```
