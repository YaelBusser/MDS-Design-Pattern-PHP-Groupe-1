# Façade

## Design pattern de manière globale :
Le Façade est un design pattern structurel qui fournit une interface simplifiée à un ensemble complexe de classes, une bibliothèque ou un framework. L'objectif est de masquer la complexité sous-jacente en offrant une interface simple aux clients, facilitant ainsi l'utilisation du système sous-jacent.

## Avantages :
1. **Simplicité d'utilisation** : Réduit la complexité pour les clients en offrant une interface facile à utiliser pour un système complexe.
2. **Isolation** : Isolent les clients de l'ensemble des dépendances complexes, diminuant le couplage entre les systèmes.
3. **Point d'entrée unique** : Fournit un point d'entrée unique pour le niveau supérieur de fonctionnalité, facilitant la gestion et l'utilisation.

## Inconvénients :
1. **Risque de surutilisation** : Peut devenir un objet god qui est trop utilisé, pour lequel tout passe par la façade, rendant le système difficile à décomposer en plus petites parties.
2. **Limitation de fonctionnalités** : Les clients peuvent être limités aux fonctionnalités fournies par la façade, sans accès direct aux fonctionnalités complexes sous-jacentes.

## Représentation UML :
![Image Façade UML](URL_vers_l'image_UML)

## Implémentation en PHP :
```php
// Système complexe
class SubsystemOne {
    public function operationOne() { return "SubsystemOne: Ready\n"; }
    public function operationN() { return "SubsystemOne: Go!\n"; }
}

class SubsystemTwo {
    public function operationOne() { return "SubsystemTwo: Get set\n"; }
    public function operationZ() { return "SubsystemTwo: Go!\n"; }
}

// Façade
class Facade {
    protected $subsystemOne;
    protected $subsystemTwo;

    public function __construct(SubsystemOne $subsystemOne, SubsystemTwo $subsystemTwo) {
        $this->subsystemOne = $subsystemOne ?? new SubsystemOne();
        $this->subsystemTwo = $subsystemTwo ?? new SubsystemTwo();
    }

    public function operation() {
        $result = "Facade initializes subsystems:\n";
        $result .= $this->subsystemOne->operationOne();
        $result .= $this->subsystemTwo->operationOne();
        $result .= "Facade orders subsystems to perform the action:\n";
        $result .= $this->subsystemOne->operationN();
        $result .= $this->subsystemTwo->operationZ();
        return $result;
    }
}

// Client code
$facade = new Facade(new SubsystemOne(), new SubsystemTwo());
echo $facade->operation();
```
