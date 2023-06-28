Padrão que divide um processo em diversos passos em uma classe principal junto com uma função responsável por seguir todos os passos em ordem e permite que subclasses alterem o comportamento de um ou mais passos mas não da ordem em si

Dessa forma teremos uma superclasse com diversas funções abstratas contendo ou não um comportamento padrão e uma função responsavel por chamar cada uma delas em ordem

Teremos também diversas subclasses que irão alterar o comportamento de alguns passos de acordo com a necessidade de cada uma

Muito útil em caso de classes que tem quase o mesmo algoritimo mas com pequenas alterações


## Exemplo

Para aplicarmos o método template, devemos começar criando nossa classe de contexto. Essa classe deve ser abstrata, conter uma função responsável por rodar todos os passos sendo, cada passo uma função abstrata

```php
abstract class AbstractClass
{
    
    final public function templateMethod(): void
    {
        $this->baseOperation1();
        $this->requiredOperations1();
        $this->baseOperation2();
        $this->hook1();
        $this->requiredOperation2();
        $this->baseOperation3();
        $this->hook2();
    }

    protected function baseOperation1(): void
    {
        echo "AbstractClass says: I am doing the bulk of the work\n";
    }

    protected function baseOperation2(): void
    {
        echo "AbstractClass says: But I let subclasses override some operations\n";
    }

    protected function baseOperation3(): void
    {
        echo "AbstractClass says: But I am doing the bulk of the work anyway\n";
    }

    abstract protected function requiredOperations1(): void;

    abstract protected function requiredOperation2(): void;

    /**
     * These are "hooks." Subclasses may override them, but it's not mandatory
     * since the hooks already have default (but empty) implementation. Hooks
     * provide additional extension points in some crucial places of the
     * algorithm.
     */
    protected function hook1(): void { }

    protected function hook2(): void { }
}

```

Entre os passos podemos ter alguns com um comportamento padrão que não precisam ser sobrescritos e passos sendo apenas uma função vazia, esses devem ser sobrescritos pelas subclasses.
Também teremos os hooks que são funções vazias mas as subclasses não são obrigadas a sobrescrevê-las. Elas servem apenas para adionar algum comportamento a mais em algumas etapas.

Criamos então nossas classes concretas que irão extender a classe principal e adicionar seus comportamentos nos passos que forem necessários

```php
class ConcreteClass1 extends AbstractClass
{
    protected function requiredOperations1(): void
    {
        echo "ConcreteClass1 says: Implemented Operation1\n";
    }

    protected function requiredOperation2(): void
    {
        echo "ConcreteClass1 says: Implemented Operation2\n";
    }
}

class ConcreteClass2 extends AbstractClass
{
    protected function requiredOperations1(): void
    {
        echo "ConcreteClass2 says: Implemented Operation1\n";
    }

    protected function requiredOperation2(): void
    {
        echo "ConcreteClass2 says: Implemented Operation2\n";
    }

    protected function hook1(): void
    {
        echo "ConcreteClass2 says: Overridden Hook1\n";
    }
}
```


Então para usarmos nosso template, precisamos apenas instanciar uma das classes concretas e chamar a função responsável por rodar todos os passos

```php
function clientCode(AbstractClass $class)
{
    $class->templateMethod();
}

echo "Same client code can work with different subclasses:\n";
clientCode(new ConcreteClass1());
echo "\n";

echo "Same client code can work with different subclasses:\n";
clientCode(new ConcreteClass2());
```

E como resultado teremos 
```txt
Same client code can work with different subclasses:
AbstractClass says: I am doing bulk of the work
ConcreteClass1 says: Implemented Operation1
AbstractClass says: But I let subclasses to override some operations
ConcreteClass1 says: Implemented Operation2
AbstractClass says: But I am doing bulk of the work anyway

Same client code can work with different subclasses:
AbstractClass says: I am doing bulk of the work
ConcreteClass2 says: Implemented Operation1
AbstractClass says: But I let subclasses to override some operations
ConcreteClass2 says: Overridden Hook1
ConcreteClass2 says: Implemented Operation2
AbstractClass says: But I am doing bulk of the work anyway
```