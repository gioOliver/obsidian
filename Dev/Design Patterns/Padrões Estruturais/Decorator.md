Padrão que permite adicionar novos comportamentos a objetos por envolver eles em objetos "envelopadores/embrulhadores" que contém esses comportamentos

Serve com uma alternativa á herança ou a [[Classe Abstrata]] pois, nos dois casos, quando for preciso usar mais de um comportamento/subclasse, será necessário criar outra classe que una os comportamentos necessário. Existe também o fato de não ser possível alterar um comportamento de um objeto durante a excecução, seria necessário substituí-lo completamente.

No caso do Decorator você vai só adicionando comportamento em cima de comportamento e, no fim, tudo acontece do jeitinho que deveria acontecer.

## Conteúdo

- A interface: define as funções que existirão tanto nos wrappers quanto nos objetos a serem decorados
- O objeto base: O objeto que possui o comportametno principal e será envolto por outros objetos
- O decorador base: classe abstrata que possui o comportamento padrão dos wrappers
- Os wrappers/decorators: Herdam do decorador base e adicionam seus próprios comportamentos ao objeto base
- O Cliente, responsavel por instanciar o objeto base e envolvêlo em todos os wrappers que forem necessários

## Exemplo

Peimeiro de tudo, criaremos nossa interface apenas com a função a ser implementada por todos os objetos participantes do decorator

```php
interface Component
{
    public function operation(): string;
}
```

Criamos então nosso objeto base que implementa a interface e pode possuir diversas outras funções
```php
class ConcreteComponent implements Component
{
    public function operation(): string
    {
        return "ConcreteComponent";
    }
}
```

No nosso decorador base, além de seguirmos a interface, definiremos no constructor um método para adicionar outro decorator numa espécie de pilha.

```php
class Decorator implements Component
{
    
    protected $component;

    public function __construct(Component $component)
    {
        $this->component = $component;
    }

  
    public function operation(): string
    {
        return $this->component->operation();
    }
}
```

Criamos então nossos decorators que irão seguir o decorator básico e alterar seu comportamento
```php

class ConcreteDecoratorA extends Decorator
{
    public function operation(): string
    {
        return "ConcreteDecoratorA(" . parent::operation() . ")";
    }
}

class ConcreteDecoratorB extends Decorator
{
    public function operation(): string
    {
        return "ConcreteDecoratorB(" . parent::operation() . ")";
    }
}
```

O Cliente consegue passar por todas as camadas de um decorator  independente de quantas camasas possui, ele também não precisa estar ciente do comportamento de cada camada
```php
function clientCode(Component $component)
{
    echo "RESULT: " . $component->operation();
}
```

Dessa maneira o cliente consegue trabalhar tanto com objetos simples
```php
$simple = new ConcreteComponent();
echo "Client: I've got a simple component:\n";
clientCode($simple);
echo "\n\n";

```

Quanto com objetos mais complexos e decorados
```php
$decorator1 = new ConcreteDecoratorA($simple);
$decorator2 = new ConcreteDecoratorB($decorator1);
echo "Client: Now I've got a decorated component:\n";
clientCode($decorator2);
```
Nesse caso passamos o objeto simples para o primeiro decorator e o primeiro decorator no constructor do segundo decorator, dessa maneira implementamos uma pilha de comportamentos a serem executados

Como output teremos:
```txt
Client: I've got a simple component:
RESULT: ConcreteComponent

Client: Now I've got a decorated component:
RESULT: ConcreteDecoratorB(ConcreteDecoratorA(ConcreteComponent))
```