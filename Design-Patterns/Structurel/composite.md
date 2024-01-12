# Composite

## Design pattern de manière globale :
Le Composite est un design pattern structurel qui permet de composer des objets en structures d'arbre pour représenter des hiérarchies partie-tout. Ce pattern permet de traiter des objets individuels et des compositions d'objets de manière uniforme. Il est particulièrement utile pour créer une structure hiérarchique profonde, où les éléments individuels et les compositions d'éléments sont manipulés de la même façon.

## Avantages :
1. **Simplicité** : Les clients utilisent des composés et des éléments individuels de la même manière, simplifiant l'interface client.
2. **Flexibilité de la structure** : Permet de construire des structures complexes à partir de composants simples.
3. **Facilité d'ajout de nouveaux types de composants** : Il est facile d'ajouter de nouveaux types tant qu'ils supportent l'interface commune.

## Inconvénients :
1. **Conception plus complexe** : Peut rendre la conception du système plus complexe, car il faut garder une interface commune entre les composants.
2. **Difficulté potentielle à restreindre les composants** : Il peut être difficile de restreindre les types de composants que certains composés peuvent accepter.
3. **Surcharge de performance** : Peut entraîner une surcharge de performance si l'arbre est très profond ou très large.

## Représentation UML :
![Image](https://media.discordapp.net/attachments/884824217110061117/1195362453538742283/image.png)

## Implémentation en PHP :
```php
// Component
abstract class Component {
    public function add(Component $component) { /* ... */ }
    public function remove(Component $component) { /* ... */ }
    public function getChild($index) { /* ... */ }
    abstract public function operation(): string;
}

// Leaf
class Leaf extends Component {
    public function operation(): string {
        return "Leaf";
    }
}

// Composite
class Composite extends Component {
    protected $children = [];

    public function add(Component $component) {
        $this->children[] = $component;
    }

    public function remove(Component $component) {
        $this->children = array_filter($this->children, function($child) use ($component) {
            return $child !== $component;
        });
    }

    public function getChild($index): Component {
        return $this->children[$index];
    }

    public function operation(): string {
        $results = [];
        foreach ($this->children as $child) {
            $results[] = $child->operation();
        }
        return "Branch(" . join(", ", $results) . ")";
    }
}

// Utilisation du Composite
$leaf1 = new Leaf();
$leaf2 = new Leaf();
$composite = new Composite();

$composite->add($leaf1);
$composite->add($leaf2);

echo $composite->operation();


