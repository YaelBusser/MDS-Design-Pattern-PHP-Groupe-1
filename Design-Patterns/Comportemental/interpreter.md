# Interpréteur (Interpreter)

## Design pattern de manière globale :
L'Interpréteur est un design pattern comportemental qui définit une représentation grammaticale pour une langue et un interpréteur qui utilise cette représentation pour interpréter des phrases dans la langue. Il est souvent utilisé pour des langages de programmation, des moteurs de règles, et des processeurs de commandes.

## Avantages :
1. **Extensibilité** : Facile à étendre et modifier les règles grammaticales ou les opérations.
2. **Séparation des préoccupations** : Sépare clairement la grammaire des opérations, améliorant la maintenabilité.
3. **Réutilisabilité** : Les expressions peuvent être réutilisées dans différentes parties de l'interprétation.

## Inconvénients :
1. **Complexité** : Peut devenir complexe et difficile à gérer pour des grammaires larges ou complexes.
2. **Performance** : Peut être moins efficace que d'autres méthodes de parsing pour des langages complexes.
3. **Difficulté de débogage** : Les erreurs dans l'interprétation peuvent être difficiles à tracer et à corriger.

## Représentation UML :
![Image Interpréteur UML](URL_vers_l'image_UML)

## Implémentation en PHP :
```php
// Interface Expression
interface Expression {
    public function interpret(array $context): bool;
}

// TerminalExpression
class TerminalExpression implements Expression {
    private $data;

    public function __construct(string $data) {
        $this->data = $data;
    }

    public function interpret(array $context): bool {
        return in_array($this->data, $context);
    }
}

// OrExpression
class OrExpression implements Expression {
    private $expr1;
    private $expr2;

    public function __construct(Expression $expr1, Expression $expr2) {
        $this->expr1 = $expr1;
        $this->expr2 = $expr2;
    }

    public function interpret(array $context): bool {
        return $this->expr1->interpret($context) || $this->expr2->interpret($context);
    }
}

// AndExpression
class AndExpression implements Expression {
    private $expr1;
    private $expr2;

    public function __construct(Expression $expr1, Expression $expr2) {
        $this->expr1 = $expr1;
        $this->expr2 = $expr2;
    }

    public function interpret(array $context): bool {
        return $this->expr1->interpret($context) && $this->expr2->interpret($context);
    }
}

// Client code
$context = ['John', 'Doe'];

// John OR Doe
$isJohnOrDoe = new OrExpression(new TerminalExpression('John'), new TerminalExpression('Doe'));
echo $isJohnOrDoe->interpret($context) ? 'True ' : 'False '; // Outputs: True

// John AND Jane
$isJohnAndJane = new AndExpression(new TerminalExpression('John'), new TerminalExpression('Jane'));
echo $isJohnAndJane->interpret($context) ? 'True ' : 'False '; // Outputs: False
```
