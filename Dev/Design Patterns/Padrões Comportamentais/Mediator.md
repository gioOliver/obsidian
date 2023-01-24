Padrão de design que ajuda a diminuir a dependência caótica entre objetos fazendo com que eles se comuniquem uns com os outros apenas através de um mediador. Um bom padrão para diminuir o [[Acoplamento]] entre classes.

Para aplicarmos o mediador em umm aglomerado de classes, devemos criar primeiro uma interface para ele apenas com o metodo notify

```php
interface Mediator
{
    public function notify(object $sender, string $event): void;
}
```


Criamos então o mediador em si, onde, em seu constructor, devemos instanciar todas as classes que irão se comunicar e em notify, receberemos o objeto responsável por chamar o mediador e o evento que ele quer disparar

```php
class ConcreteMediator implements Mediator
{
    private $component1;

    private $component2;

    public function __construct(Component1 $c1, Component2 $c2)
    {
        $this->component1 = $c1;
        $this->component1->setMediator($this);
        $this->component2 = $c2;
        $this->component2->setMediator($this);
    }

    public function notify(object $sender, string $event): void
    {
        if ($event == "A") {
            echo "Mediator reacts on A and triggers following operations:\n";
            $this->component2->doC();
        }

        if ($event == "D") {
            echo "Mediator reacts on D and triggers following operations:\n";
            $this->component1->doB();
            $this->component2->doC();
        }
    }
}
```

Em notify, é verificado o evento envido e então será feito o processamento necessário

criamos então um componente base que terá os métodos padrão dos componentes

``` php
class BaseComponent
{
    protected $mediator;

    public function __construct(Mediator $mediator = null)
    {
        $this->mediator = $mediator;
    }

    public function setMediator(Mediator $mediator): void
    {
        $this->mediator = $mediator;
    }
}
```


E então criamos os componentes em si, contendo métodos que farão qualquer outra coisa e métodos que irão chamar o mediador para processar o que eles precisam de outros métodos

```php
class Component1 extends BaseComponent
{
    public function doA(): void
    {
        echo "Component 1 does A.\n";
        $this->mediator->notify($this, "A");
    }

    public function doB(): void
    {
        echo "Component 1 does B.\n";
        $this->mediator->notify($this, "B");
    }
}

class Component2 extends BaseComponent
{
    public function doC(): void
    {
        echo "Component 2 does C.\n";
        $this->mediator->notify($this, "C");
    }

    public function doD(): void
    {
        echo "Component 2 does D.\n";
        $this->mediator->notify($this, "D");
    }
}
```
Dessa maneira nenhum componente sabe o que faz outro componente e nem qual componente será chamado para realizar a tarefa que foi mandada ao mediador.

No client code então teremos as chamadas dos objetos onde cada um chama uma função onde será enviado um comando para o mediador enviar a outra classe
```php
$c1 = new Component1();
$c2 = new Component2();
$mediator = new ConcreteMediator($c1, $c2);

echo "Client triggers operation A.\n";
$c1->doA();

echo "\n";
echo "Client triggers operation D.\n";
$c2->doD();
```


No final, teremos um output parecido com
```txt
Client triggers operation A.
Component 1 does A.
Mediator reacts on A and triggers following operations:
Component 2 does C.

Client triggers operation D.
Component 2 does D.
Mediator reacts on D and triggers following operations:
Component 1 does B.
Component 2 does C.
```