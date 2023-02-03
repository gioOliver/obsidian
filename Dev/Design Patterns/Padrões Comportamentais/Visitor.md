Consiste em uma classe Visitor com um comportamento específico que pode ser aplicado a várias outras classes que não tem nada a ver uma com a outra. Essa classe então visita outras classes e executa seu comportamento de maneira personalizada para cada uma das classes

## Composição

Uma classe Visitor que implementa uma interface Visitor. Essa interface deve ter todos os metodos personalizados que o Visitor irá realizar em cada classe;

Classes diversas que, que irão receber esse Visitor, implementam uma interface Element que possui o método `accept`. O método `accept` é responsavel por receber o Visitor e chamar a function que tem a personalização do comportamento adequado para sí.

Muito útil caso haja diversas classes no sistema que devam ser exportadas em arquivos de extensões diferentes
Nesse caso, cada extenção seria um Visitor diferente, teriamos por exemplo `ExportPDF`, `ExportCSV`, `ExportExcel`, etc. E todas as classes que for necessário exportar terão uma função `accept` para receber o visitor e executar a função para se exportar


## Exemplo

Começamos então criando a interface para que todas as classes que serão visitadas implementem
```php
interface Component
{
    public function accept(Visitor $visitor): void;
}
```

E, em cada Classe, implementamos a função `accept` para chamar a função certa do Visitor
```php
class ConcreteComponentA implements Component
{
    public function accept(Visitor $visitor): void
    {
        $visitor->visitConcreteComponentA($this);
    }

    public function exclusiveMethodOfConcreteComponentA(): string
    {
        return "A";
    }
}

class ConcreteComponentB implements Component
{
    public function accept(Visitor $visitor): void
    {
        $visitor->visitConcreteComponentB($this);
    }

    public function specialMethodOfConcreteComponentB(): string
    {
        return "B";
    }
}
```
cada classe terá suas funções e comportamentos específicos e que podem ser acessados pelas funções personalizadas do Visitor´.

Criamos então a inteface do Visitor. Sempre que uma nova classe passar a recever o Visitor, deve-se adicionar uma função nova para classe
```php
interface Visitor
{
    public function visitConcreteComponentA(ConcreteComponentA $element): void;

    public function visitConcreteComponentB(ConcreteComponentB $element): void;
}
```

Criamos então nossos Visitors, com cada função acessando métodos diferentes das classes que visitam
```php
class ConcreteVisitor1 implements Visitor
{
    public function visitConcreteComponentA(ConcreteComponentA $element): void
    {
        echo $element->exclusiveMethodOfConcreteComponentA() . " + ConcreteVisitor1\n";
    }

    public function visitConcreteComponentB(ConcreteComponentB $element): void
    {
        echo $element->specialMethodOfConcreteComponentB() . " + ConcreteVisitor1\n";
    }
}

class ConcreteVisitor2 implements Visitor
{
    public function visitConcreteComponentA(ConcreteComponentA $element): void
    {
        echo $element->exclusiveMethodOfConcreteComponentA() . " + ConcreteVisitor2\n";
    }

    public function visitConcreteComponentB(ConcreteComponentB $element): void
    {
        echo $element->specialMethodOfConcreteComponentB() . " + ConcreteVisitor2\n";
    }
}
```

No ClientCode, normalmente, receberemos uma lista dos objetos a serem visitados e qual Visitor será usado.
```php
function clientCode(array $components, Visitor $visitor)
{
    // ...
    foreach ($components as $component) {
        $component->accept($visitor);
    }
    // ...
}

$components = [
    new ConcreteComponentA(),
    new ConcreteComponentB(),
];

echo "The client code works with all visitors via the base Visitor interface:\n";
$visitor1 = new ConcreteVisitor1();
clientCode($components, $visitor1);
echo "\n";

echo "It allows the same client code to work with different types of visitors:\n";
$visitor2 = new ConcreteVisitor2();
clientCode($components, $visitor2);
```

E como output, teremos
```php
The client code works with all visitors via the base Visitor interface:
A + ConcreteVisitor1
B + ConcreteVisitor1

It allows the same client code to work with different types of visitors:
A + ConcreteVisitor2
B + ConcreteVisitor2
```