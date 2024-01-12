# Pont (Bridge)

## Design pattern de manière globale :
Le Pont est un design pattern structurel qui sépare l'abstraction d'une entité de son implémentation, de sorte que les deux puissent varier indépendamment. Ce pattern est utile pour éviter un couplage rigide entre l'abstraction et son implémentation, ce qui permet d'étendre les deux indépendamment sans affecter l'autre. Il est particulièrement utile dans les cas où une entité peut avoir plusieurs variantes, et on souhaite éviter une hiérarchie d'héritage encombrée.

## Avantages :
1. **Flexibilité accrue** : Permet de changer l'implémentation sans perturber l'abstraction et vice-versa.
2. **Principe d'ouverture/fermeture** : Les abstractions et les implémentations peuvent être développées et étendues indépendamment.
3. **Réduction de la taille de la hiérarchie des classes** : Évite de créer des hiérarchies de classes étendues pour chaque combinaison d'abstraction et d'implémentation.

## Inconvénients :
1. **Complexité accrue** : Peut augmenter la complexité du code en introduisant plusieurs nouvelles couches.
2. **Difficulté de compréhension initiale** : Peut être plus difficile à comprendre pour les nouveaux développeurs en raison de la séparation entre abstractions et implémentations.
3. **Coût initial** : Le coût initial de mise en place de la structure peut être plus élevé en raison de la planification supplémentaire nécessaire.

## Représentation UML :

## Implémentation en PHP :
```php
// Implementor
interface Implementor {
    public function operationImpl(): string;
}

// ConcreteImplementor A
class ConcreteImplementorA implements Implementor {
    public function operationImpl(): string {
        return "Implémentation ConcreteImplementor A.";
    }
}

// ConcreteImplementor B
class ConcreteImplementorB implements Implementor {
    public function operationImpl(): string {
        return "Implémentation ConcreteImplementor B.";
    }
}

// Abstraction
abstract class Abstraction {
    protected $implementor;

    public function __construct(Implementor $implementor) {
        $this->implementor = $implementor;
    }

    public function operation(): string {
        return "Abstraction: Base operation with:\n" . $this->implementor->operationImpl();
    }
}

// RefinedAbstraction
class RefinedAbstraction extends Abstraction {
    public function operation(): string {
        return "RefinedAbstraction: Extended operation with:\n" . $this->implementor->operationImpl();
    }
}

// Utilisation du Bridge
$implementorA = new ConcreteImplementorA();
$abstractionA = new RefinedAbstraction($implementorA);
echo $abstractionA->operation();

$implementorB = new ConcreteImplementorB();
$abstractionB = new RefinedAbstraction($implementorB);
echo $abstractionB->operation();
```
