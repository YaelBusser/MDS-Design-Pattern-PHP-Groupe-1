# Adaptateur (Adapter)

## Design pattern de manière globale :
L'Adapter est un design pattern structurel qui permet à des interfaces incompatibles de travailler ensemble. Il agit en tant qu'intermédiaire, convertissant l'interface d'une classe existante en une autre interface attendue par les clients. Cela est utile pour intégrer des classes anciennes ou incompatibles dans de nouvelles architectures sans modifier leur code source.

## Avantages :
1. **Intercompatibilité** : Permet à des classes ayant des interfaces différentes de collaborer.
2. **Réutilisation du code** : Facilite la réutilisation de classes existantes même si elles ne correspondent pas exactement aux besoins actuels.
3. **Séparation des préoccupations** : Sépare le code de la classe existante du code d'adaptation, respectant ainsi le principe de responsabilité unique.

## Inconvénients :
1. **Complexité supplémentaire** : Introduit des couches additionnelles, rendant parfois le système plus complexe.
2. **Rigidité** : Peut limiter la flexibilité en forçant l'adaptation à une interface spécifique.
3. **Compréhension** : Nécessite une compréhension claire du fonctionnement des deux interfaces pour implémenter correctement l'adaptateur.

## Représentation UML :
!(Image)[https://media.discordapp.net/attachments/884824217110061117/1195348096331288596/image.png]
## Implémentation en PHP :
```php
// Interface cible
interface Target {
    public function request(): string;
}

// Classe à adapter
class Adaptee {
    public function specificRequest(): string {
        return "Spécificité de l'Adaptee.";
    }
}

// L'Adapter
class Adapter implements Target {
    private $adaptee;

    public function __construct(Adaptee $adaptee) {
        $this->adaptee = $adaptee;
    }

    public function request(): string {
        return "Adapter: (traduit) " . $this->adaptee->specificRequest();
    }
}

// Utilisation de l'Adapter
function clientCode(Target $target) {
    echo $target->request();
}

$adaptee = new Adaptee();
echo "Adaptee: " . $adaptee->specificRequest() . "\n";

$adapter = new Adapter($adaptee);
clientCode($adapter);
```

