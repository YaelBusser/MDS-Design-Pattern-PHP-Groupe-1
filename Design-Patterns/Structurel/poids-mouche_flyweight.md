# Design pattern de manière globale :
L'objectif est de mettre en cache les données identiques chez différents objets

# Avantages :
Réduit considérablement la RAM

# Inconvénients : 
- Perte en cycles microprocesseur
- Code qui devient compliqué
  
# Représentation UML : 
<img src="C:\Users\mrtbg\OneDrive\Documents\DEV\COURS\B3DEV\Design Pattern\flyWeight\flyWeight.png">

# Implémentation en PHP :
``` php
<?php

class TShirtFlyweight
{
    private string $description;
    private string $image;
    private float $price;

    public function __construct(string $description, string $image, float $price)
    {
        $this->description = $description;
        $this->image = $image;
        $this->price = $price;
    }

    public function getDescription(): string
    {
        return $this->description;
    }

    public function getImage(): string
    {
        return $this->image;
    }

    public function getPrice(): float
    {
        return $this->price;
    }
}

class TShirt
{
    private TShirtFlyweight $flyweight;
    private string $color;
    private string $size;

    public function __construct(TShirtFlyweight $flyweight, string $color, string $size)
    {
        $this->flyweight = $flyweight;
        $this->color = $color;
        $this->size = $size;
    }

    public function getColor(): string
    {
        return $this->color;
    }

    public function getSize(): string
    {
        return $this->size;
    }

    public function getFlyweight(): TShirtFlyweight
    {
        return $this->flyweight;
    }

    public function displayInfo(): string
    {
        return sprintf(
            "Couleur: %s, Taille: %s, Description: %s, Image: %s, Prix: %.2f",
            $this->getColor(),
            $this->getSize(),
            $this->getFlyweight()->getDescription(),
            $this->getFlyweight()->getImage(),
            $this->getFlyweight()->getPrice()
        );
    }
}

class TShirtFactory
{
    private array $flyweights = [];

    public function getFlyweight(string $description, string $image, float $price): TShirtFlyweight
    {
        $key = md5($description . $image . $price);

        if (!isset($this->flyweights[$key])) {
            $this->flyweights[$key] = new TShirtFlyweight($description, $image, $price);
        }

        return $this->flyweights[$key];
    }
}

$factory = new TShirtFactory();
$flyweight = $factory->getFlyweight('Cool T-Shirt', 'image.png', 19.99);

$tshirt1 = new TShirt($flyweight, 'rouge', 'M');
$tshirt2 = new TShirt($flyweight, 'bleu', 'L');
$tshirt3 = new TShirt($flyweight, 'vert', 'S');

echo $tshirt1->displayInfo() . PHP_EOL;
echo $tshirt2->displayInfo() . PHP_EOL;
echo $tshirt3->displayInfo() . PHP_EOL;
```

