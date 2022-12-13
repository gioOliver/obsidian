
Usado para evitar o alto nivel de [[Acoplamento]] de um sistema. Dessa forma, ao inves de uma classe instanciar outra classe. A classe recebe a outra classe em um de seus métodos ou no construtor. 


Esse método é  uma das soluções para o [[Dependency Inversion Principle]] do SOLID

Seria algo do tipo

```php

class carro {
	public Roda $roda;
	public Motor $motor;

	__constructor(){
		$this->roda = new Roda('marca', 'aro');
		$this->motor = new Motor('tipo', 'qtd_cavalos');
	}
}


```

Dessa maneira a classe acaba ficando com um nível alto de acoplamento. Se algum dia os construtores das classes roda ou motor forem alterados, a classe Carro deixará de funcionar.

Outro problema seria na hora de realizar testes unitários por algum motivo que eu não pesquisei o suficiente, mas ajuda, confia.

para resolver essa situação, podemos usar 3 tipos de injeção de dependência:

## Injeção por Constructor

``` php
class carro {
	private Roda $roda;
	private Motor $motor;

	__constructor(Roda $roda, Motor $motor){
		$this->roda = $roda;
		$this->motor = $motor;
	}
}

class carroController
{
	public function criaCarro(){
		$roda = new Roda('marca', 'aro');
		$motor = new Motor('tipo', 'qtd_cavalos');

		$carro = new Carro($roda, $motor);
	}
}

```

Dessa maneira, a classe que vamos utilizar recebe via constructor todas as classes que ela mesmo ira usar em sua execução.

## Injeção por propriedade (setter/getter)

Ao invés de setar as classes direto no construtor da classe principal, pode se criar um método set na classe principal para que ele acidione a classe secundária a si mesma 

``` php
class carro {
	private Roda $roda;
	private Motor $motor;

	public function setRoda(Roda $roda)
	{
		$this->roda = $roda;
	}

	public function setMotor(Motor $motor)
	{
		$this->motor = $motor;
	}

}

class carroController
{
	public function criaCarro(){
		$roda = new Roda('marca', 'aro');
		$motor = new Motor('tipo', 'qtd_cavalos');

		$carro = new Carro($roda, $motor);
		
		$carro->setRoda($roda);
		$carro->setMotor($motor);
	}
}
```




## Injeção por interface

Ainda não entendi bem o rolê dessa aqui, mas no geral dá para passar as dependencias via interface uhul
