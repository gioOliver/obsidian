Também conhecido por Chain of Command, a cadeia de responsabilide consite em várias pequenas classes (Handlers) contendo apenas uma regra onde, ao receber uma requisição a classe decide se o conteúdo da requisição se aplica a sua regra ou não

Caso se aplique, a classe processa a requisição e retorna algo, se não, ela passa a requisição para a próxima classe e assim por diante.

A cadeia de responsabilidade pode ser usada tanto de maneira onde cada regra pode processar o conteúdo e então passá-lo para a próxima regra quanto de maneira onde ou apenas uma regra se aplica, ou nenhuma.

A cadeia de respossabilidade é muito útil para substituir blocos de ifs em funções e, ao extrair uma regra para uma classe, possibilita também a reutilização de código

É essencial que todos os handlers implementem a mesma interface que contenha apenas o método execute. Em alguns casos pode haver o método setNext que recebe o próximo handler da cadeia. Deve-se também haver um Handler abstrato contendo o comportamento básico dos handlers

## Exemplo

- Primeiro criamos a interface que será usada por todos os handlers
``` php
interface Handler
{
    public function setNext(Handler $handler): Handler;

    public function handle(string $request): ?string;
}
```

- Criamos então uma [[Classe Abstrata]] para os handlers e que implementa os métodos da interface. Implementa-se o setNext já na classe abstrata para que possamos utilizar o encadeamento de funções `$classe->setNext($handler1)->setNext($handler2)->setNext($handler3)`;
``` php
abstract class AbstractHandler implements Handler
{
    private $nextHandler;

    public function setNext(Handler $handler): Handler
    {
        $this->nextHandler = $handler;
        return $handler;
    }

    public function handle(string $request): ?string
    {
        if ($this->nextHandler) {
            return $this->nextHandler->handle($request);
        }

        return null;
    }
}
```

- Implementamos os handlers no padrão onde ou um handler aplica sua regra ou nenhum aplica
``` php
class MonkeyHandler extends AbstractHandler
{
    public function handle(string $request): ?string
    {
        if ($request === "Banana") {
            return "Monkey: I'll eat the " . $request . ".\n";
        } else {
            return parent::handle($request);
        }
    }
}

class SquirrelHandler extends AbstractHandler
{
    public function handle(string $request): ?string
    {
        if ($request === "Nut") {
            return "Squirrel: I'll eat the " . $request . ".\n";
        } else {
            return parent::handle($request);
        }
    }
}

class DogHandler extends AbstractHandler
{
    public function handle(string $request): ?string
    {
        if ($request === "MeatBall") {
            return "Dog: I'll eat the " . $request . ".\n";
        } else {
            return parent::handle($request);
        }
    }
}
```

- A função responsável por executar a cadeia de responsabilidade normalmente recebe apenas um handler e, na maior parte das vezes, ela nem sabe que o handler faz parte de uma cadeia
``` php
function clientCode(Handler $handler)
{
    foreach (["Nut", "Banana", "Cup of coffee"] as $food) {
    
        echo "Client: Who wants a " . $food . "?\n";
        $result = $handler->handle($food);
        
        if ($result) {
            echo "  " . $result;
        } else {
            echo "  " . $food . " was left untouched.\n";
        }
    }
}
```


- Quando for instanciar Cliente, é necessário que seja instanciado antes todos os handlers que serão utilizados e então linkados na ordem que for necessário

``` php
class Controller{

	//finge que é java kkkkkkkkkk
	function main()
	{
		$monkey   = new MonkeyHandler();
		$squirrel = new SquirrelHandler();
		$dog      = new DogHandler();
		
		$monkey->setNext($squirrel)->setNext($dog);
	}

}
```

- Então instanciamos o client e passamos para ele o primeiro handler que fará a verificação e então é só deixar a mágica acontecer

``` php
class Controller{

	//finge que é java kkkkkkkkkk
	function main()
	{
		$monkey   = new MonkeyHandler();
		$squirrel = new SquirrelHandler();
		$dog      = new DogHandler();
		
		$monkey->setNext($squirrel)->setNext($dog);

		echo "Chain: Monkey > Squirrel > Dog\n\n";
		$client = new ClientCode($monkey);
	}

}```

- Não é obrigatório que passemos o primeiro handler da cadeia, podemos passar qualquer um dos handlers que o sistema ira seguir a cadeia a partir do handler enviado
```php
echo "Subchain: Squirrel > Dog\n\n";
$client = new ClientCode($squirrel);
```

