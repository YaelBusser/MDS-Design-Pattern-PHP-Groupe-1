# Visiteur (Visitor)

## Design pattern de manière globale :
Le Visiteur est un design pattern comportemental qui permet d'ajouter de nouvelles opérations à une structure d'objets sans modifier les classes de ces objets. Il fonctionne en séparant un algorithme des objets sur lesquels il opère, ce qui facilite l'ajout de fonctionnalités sans réécrire ou modifier les classes existantes.

## Avantages :
1. **Extension facile** : Permet d'ajouter de nouvelles opérations spécifiques à des classes sans les modifier.
2. **Regroupement d'opérations** : Regroupe les opérations sur des objets dans une seule classe.
3. **Visiteurs multiples** : Permet d'utiliser différents visiteurs pour effectuer différentes opérations sur un ensemble d'objets.

## Inconvénients :
1. **Violation d'encapsulation** : Nécessite que le visiteur ait accès aux éléments internes des objets visités.
2. **Difficulté à ajouter de nouveaux types d'éléments** : Si de nouveaux types d'éléments sont ajoutés fréquemment, le pattern peut devenir lourd à gérer car tous les visiteurs doivent être mis à jour.
3. **Complexité** : Peut rendre le code plus complexe et plus difficile à comprendre pour les nouveaux développeurs.

## Représentation UML :
![Image Visiteur UML](URL_vers_l'image_UML)

## Implémentation en PHP :
```php
// Interface Visitable
interface Visitable {
    public function accept(Visitor $visitor): void;
}

// Interface Visitor
interface Visitor {
    public function visitConcreteElementA(ConcreteElementA $elementA): void;
    public function visitConcreteElementB(ConcreteElementB $elementB): void;
}

// Concrete Elements
class ConcreteElementA implements Visitable {
    public function accept(Visitor $visitor): void {
        $visitor->visitConcreteElementA($this);
    }
    public function operationA(): string {
        return "ConcreteElementA operation";
    }
}

class ConcreteElementB implements Visitable {
    public function accept(Visitor $visitor): void {
        $visitor->visitConcreteElementB($this);
    }
    public function operationB(): string {
        return "ConcreteElementB operation";
    }
}

// Concrete Visitor
class ConcreteVisitor implements Visitor {
    public function visitConcreteElementA(ConcreteElementA $elementA): void {
        echo $elementA->operationA() . " visited by ConcreteVisitor\n";
    }
    public function visitConcreteElementB(ConcreteElementB $elementB): void {
        echo $elementB->operationB() . " visited by ConcreteVisitor\n";
    }
}

// Client code
$elementA = new ConcreteElementA();
$elementB = new ConcreteElementB();
$visitor = new ConcreteVisitor();

$elementA->accept($visitor);
$elementB->accept($visitor);
```
