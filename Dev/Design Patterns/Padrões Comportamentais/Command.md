Extrai toda a lógica de um command/cron/job para uma classe separada permitindo que essa lógica seja acessada através de outros pontos do código e não apenas pelo CLI

Para implementarmos o padrão command, devemos primeiro criar uma inteface com o metodo `execute` para nossos comandos

```php
namespace RefactoringGuru\Command\Conceptual;

interface Command
{
    public function execute(): void;
}
```

Então criamos classes de comandos para executar funções específicas

Os comandos podem ser simples e executarem sozinhos o que for necessário

```php
class SimpleCommand implements Command
{
    private $payload;

    public function __construct(string $payload)
    {
        $this->payload = $payload;
    }

    public function execute(): void
    {
        echo "SimpleCommand: See, I can do simple things like printing (" . $this->payload . ")\n";
    }
}
```

E também podem ser mais complexos, nesses casos, o command delega suas operações para outras classes, conhecidas como receivers ou handlers, que vão executar a lógica em sí.

O comando complexo recebe então em seu construtor qual sera o handler ou os handlers que ele irá usar para delegar as terefas

```php
class ComplexCommand implements Command
{
    private $receiver;

    private $a;

    private $b;

    public function __construct(Receiver $receiver, string $a, string $b)
    {
        $this->receiver = $receiver;
        $this->a = $a;
        $this->b = $b;
    }

    public function execute(): void
    {
        echo "ComplexCommand: Complex stuff should be done by a receiver object.\n";
        $this->receiver->doSomething($this->a);
        $this->receiver->doSomethingElse($this->b);
    }
}
```

O receiver não implementa a interface do command e pode conter qualquer tipo de lógica e regra.
Diferentes classes do sistema podem também atuar como handler/receiver
```php
class Receiver
{
    public function doSomething(string $a): void
    {
        echo "Receiver: Working on (" . $a . ".)\n";
    }

    public function doSomethingElse(string $b): void
    {
        echo "Receiver: Also working on (" . $b . ".)\n";
    }
}
```

A classe invoker é responsavel por gerenciar os commands e receivers, é nela onde eles serão utilizados junto a outras operações 

```php
class Invoker
{
    /**
     * @var Command
     */
    private $onStart;

    /**
     * @var Command
     */
    private $onFinish;


    public function setOnStart(Command $command): void
    {
        $this->onStart = $command;
    }

    public function setOnFinish(Command $command): void
    {
        $this->onFinish = $command;
    }

    public function doSomethingImportant(): void
    {
        echo "Invoker: Does anybody want something done before I begin?\n";
        if ($this->onStart instanceof Command) {
            $this->onStart->execute();
        }

        echo "Invoker: ...doing something really important...\n";

        echo "Invoker: Does anybody want something done after I finish?\n";
        if ($this->onFinish instanceof Command) {
            $this->onFinish->execute();
        }
    }
}
```

E então no client code, ou no cotroller, a utilização dos commands será da seguinte forma

```php
$invoker = new Invoker();
$invoker->setOnStart(new SimpleCommand("Say Hi!"));
$receiver = new Receiver();
$invoker->setOnFinish(new ComplexCommand($receiver, "Send email", "Save report"));

$invoker->doSomethingImportant();
```

E como output teremos 
```txt
Invoker: Does anybody want something done before I begin?
SimpleCommand: See, I can do simple things like printing (Say Hi!)
Invoker: ...doing something really important...
Invoker: Does anybody want something done after I finish?
ComplexCommand: Complex stuff should be done by a receiver object.
Receiver: Working on (Send email.)
Receiver: Also working on (Save report.)
```