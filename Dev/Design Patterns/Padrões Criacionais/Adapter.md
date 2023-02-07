Foca na comunicação entre objetos que possuem intefaces diferentes. É um grande conversor de dados entre objetos.

Consiste em uma classe que recebe os dados de uma classe e converte os dados para o formato aceito por uma outra classe ou outa api

## Conteudo

Uma classe Cliente que é onde tudo acontece, possui a regra de negócio e tudo o que é necessário para uma funcionalidade de um sistema

Uma Interface para o adapter que contem todos os métodos necessários para a comunicação entre classes

Uma classe Service que será a classe legado, ou a classe que receberá os dados da classe Client mas não tem uma interface compativel

Uma classe Adapter que receberá os dados da Client e enviara para a Service no formato que ela aceita

## Exemplo


Começamos então definido a classe Cliente que terá um comportamento e estrutura seguindo o padrão de seu sistema atual
``` php
class Target
{
    public function request(): string
    {
        return "Target: The default target's behavior.";
    }
}
```

E também iremos definir a classe Service que possui um método útil para a Client mas seu formato é incompativel
``` php
class Adaptee
{
    public function specificRequest(): string
    {
        return ".eetpadA eht fo roivaheb laicepS";
    }
}
```

Criamos então nossa Interface que ira consumir o Service e adaptá-lo ao Client. Ele herda o comportamento do Cliente, basicamente o usa como interface, e recebe o Service no constructor.

```php
class Adapter extends Target
{
    private $adaptee;

    public function __construct(Adaptee $adaptee)
    {
        $this->adaptee = $adaptee;
    }

    public function request(): string
    {
        return "Adapter: (TRANSLATED) " . strrev($this->adaptee->specificRequest());
    }
}
```

E o clientCode por sua vez receberá qualquer instancia de Service para usar suas funções, independente se for o service em si ou se foi um adapter
```php
function clientCode(Target $target)
{
    echo $target->request();
}
```

Para usarmos cada um dos métodos:

```php
echo "Client: I can work just fine with the Target objects:\n";
$target = new Target();
clientCode($target);
echo "\n\n";

$adaptee = new Adaptee();
echo "Client: The Adaptee class has a weird interface. See, I don't understand it:\n";
echo "Adaptee: " . $adaptee->specificRequest();
echo "\n\n";

echo "Client: But I can work with it via the Adapter:\n";
$adapter = new Adapter($adaptee);
clientCode($adapter);
```

E teremos como output:
```txt
Client: I can work just fine with the Target objects:
Target: The default target's behavior.

Client: The Adaptee class has a weird interface. See, I don't understand it:
Adaptee: .eetpadA eht fo roivaheb laicepS

Client: But I can work with it via the Adapter:
Adapter: (TRANSLATED) Special behavior of the Adaptee.
```
