Padrão onde um objeto consegue mudar seu comportamento interno quando seu estado é alterado

Bom para substituir switches ou um grande numero de ifs em sequencia pois, quanto mais o sistema evolui, mais condições podem ser aplicadas e maior vai ficar 

Nesse padrão, cada if ou cada case de um switch é extraido para um aclasse de State que segue uma interface. esse objeto é responsavel por todo o comportamento específico de uma classe naquele estado e a Classe original apenas faz uma referencia à classe de estado na qual ela se encontra

Se assemelha com o padrão [[Strategy]], a diferenca é que os objetos de State podem estar cientes uns dos outros e mudar de estado diversas vezes enquanto em strategy um objeto strategy quase nunca sabe sobre outro objeto strategy

Além de cumprir o [[Single Responsibility Principle]], esse padrão segue o [[Open-Closed Principle]] pois caso seja necessário adicionar mais um if/case em seu código, é só criar uma nova classe de estado e nada do que você tinha feito antes irá quebrar

## Exemplo

### Contexto Útil

Se aplicado na conciliação de boletos em vendas podemos estabelecer estados para cada situação de venda e cada estado tendo uma função para alterar o estado atual da venda

Se o estado atual foi pago, nada acontece

Se for ativo, muda para pago

Se for vencido, é aplicado o valor de juros e de multa e então muda para pago

### Código

Primeiro definimos uma classe com o contexto da aplicação, onde será realizado todas as ações necessárias de um objeto e todas as chamadas para as ações do objetos de State

```php 
class Context
{

    private $state;

    public function __construct(State $state)
    {
        $this->transitionTo($state);
    }

    public function transitionTo(State $state): void
    {
        echo "Context: Transition to " . get_class($state) . ".\n";
        $this->state = $state;
        $this->state->setContext($this);
    }

    public function request1(): void
    {
        $this->state->handle1();
    }

    public function request2(): void
    {
        $this->state->handle2();
    }
}
```
Nesse caso, além de declararmos um estado para nossa classe, passamos também a classe em si para o estado para que ela possa ser manipulada dentro dele

Criamos então uma [[Classe Abstrata]] que será usada por todos os objetos de estado. Essa classe terá todo o comportamento em comum entre os objetos de estado como é o caso de `setContext()` que declara o contexto do estado.
```php
abstract class State
{
    protected $context;

    public function setContext(Context $context)
    {
        $this->context = $context;
    }

    abstract public function handle1(): void;

    abstract public function handle2(): void;
}
```

Por fim, criamos os objetos de estado em si, cada um com um comportamento diferente e com a possibilidade de alterarem o estado do contexto passado para eles
```php
class ConcreteStateA extends State
{
    public function handle1(): void
    {
        echo "ConcreteStateA handles request1.\n";
        echo "ConcreteStateA wants to change the state of the context.\n";
        $this->context->transitionTo(new ConcreteStateB());
    }

    public function handle2(): void
    {
        echo "ConcreteStateA handles request2.\n";
    }
}

class ConcreteStateB extends State
{
    public function handle1(): void
    {
        echo "ConcreteStateB handles request1.\n";
    }

    public function handle2(): void
    {
        echo "ConcreteStateB handles request2.\n";
        echo "ConcreteStateB wants to change the state of the context.\n";
        $this->context->transitionTo(new ConcreteStateA());
    }
}
```

Para usarmos essas funções, deveremos fazer chamadas do tipo 
```php
$context = new Context(new ConcreteStateA());
$context->request1();
$context->request2();
```

E teremos como output
``` text
Context: Transition to RefactoringGuru\State\Conceptual\ConcreteStateA.
ConcreteStateA handles request1.
ConcreteStateA wants to change the state of the context.
Context: Transition to RefactoringGuru\State\Conceptual\ConcreteStateB.
ConcreteStateB handles request2.
ConcreteStateB wants to change the state of the context.
Context: Transition to RefactoringGuru\State\Conceptual\ConcreteStateA.
```
