Uma classe abstrata se assemelha com uma interface por definir quais métodos devem ser implementados por quem a extende, a diferença é que em uma classe abstrata são definidos também os comportamentos padrões para todas as classes, assim a classe que estiver herdando seus atributos não precisa implementar todos os métodos, apenas os que forem específicos.

Uma classe abstrata não pode ser instanciada, apenas suas classes herdeiras, sendo assim, para acessar seus métodos deve se fazer algo do tipo.


```php

class ClasseAbstrata{
	public function metodoBasico()
	{
		return "retorno basico";
	}

	public function outroMetodo()
	{
		return "retorno diferente";
	}
}


class ClasseEspecifica extends classAbstrata
{
	public function outroMetodo()
	{
		return "retorno especifico";
	}
}


class controller{

	$classeEspecifica = new ClasseEspecifica();

	echo $classeEspecifica->metodoBasico(); //retorno basico

	echo $classeEspecifica->outroMetodo(); //retorno especifico

}

```

Uma da vantagens da classe abstrata é o encadeamento de funções, como acontece em [[Chain of Responsibility]] onde podemos usar algo como

```php
$class->randomFunction($param1)->randomFunction($param2)->randomFunction($param3);
```
