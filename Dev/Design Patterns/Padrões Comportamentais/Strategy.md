Permite que você isole um comportamento específico de uma classe que pode ser realizado de diversas maneiras diferentes. Cada maneira de realizar esse comportamento vira uma classe de strategy que segue uma interface strategy

O padrão consiste em uma classe de contexto que irá receber e executar uma estratégia, uma interface para estratégias, normalmente apenas com a função `execute()`, e estratégias que usam essa interface e implementem cada uma um comportamento diferente para a função `execute()`



## Exemplo


### Contexto útil

Pode muito bem ser usado para gerar parcelas de diferentes tipos de vendas

Vendas a vista geram apenas uma parcela com uma transação

Vendas parceladas no banco geram n parcelas mas com apenas uma transação

Vendas parceladas na loja geram n parcelas cada uma tendo uma transação


### Código

Primeiro, criamos nossa classe de contexto. Essa classe vai ter uma estratégia definida já no constructor mas também terá uma função setStrategy para caso seja necessário alterar a estratégia durante o processamento.

```php
class Context
{
   
    private $strategy;

    public function __construct(Strategy $strategy)
    {
        $this->strategy = $strategy;
    }

    public function setStrategy(Strategy $strategy)
    {
        $this->strategy = $strategy;
    }

    public function doSomeBusinessLogic(): void
    {
        echo "Context: Sorting data using the strategy (not sure how it'll do it)\n";
        $result = $this->strategy->doAlgorithm(["a", "b", "c", "d", "e"]);
        echo implode(",", $result) . "\n";
    }
}
```
Teremos também a função que irá utilzar a estratégia. Essa classe não tem nenhuma informação sobre o que acontece nas estratégias, apeas as chama e usa o resultado.

Definiremos então nossa interface paras as estratégias. O normal é ter só a função para executar a estratégia
```php
interface Strategy
{
    public function doAlgorithm(array $data): array;
}
```

Por fim, criaremos nossas estratégias que implementam a interface. Cada uma processando os dados recebidos de maneira diferente
```php
class ConcreteStrategyA implements Strategy
{
    public function doAlgorithm(array $data): array
    {
        sort($data);

        return $data;
    }
}

class ConcreteStrategyB implements Strategy
{
    public function doAlgorithm(array $data): array
    {
        rsort($data);

        return $data;
    }
}
```

Para utilizar as estratégias, precisamos apenas isntanciar nossa classe de contexto e enviar no construtor a classe de estratégia a ser usada 
```php
$context = new Context(new ConcreteStrategyA());
echo "Client: Strategy is set to normal sorting.\n";
$context->doSomeBusinessLogic();

echo "\n";

```

Caso seja necessario mudar de estratégia, é só usar a função serStrategy
```php
echo "Client: Strategy is set to reverse sorting.\n";
$context->setStrategy(new ConcreteStrategyB());
$context->doSomeBusinessLogic();
```

E como output teremos
```txt
Client: Strategy is set to normal sorting.
Context: Sorting data using the strategy (not sure how it'll do it)
a,b,c,d,e

Client: Strategy is set to reverse sorting.
Context: Sorting data using the strategy (not sure how it'll do it)
e,d,c,b,a
```git