Uma das regras mais simples de ser aplicada, consiste em transformar atributos de tipos primitivos como string e int em uma classe

Se a classe pessoa possui o atributo CPF e esse atributo é uma string, o aconselhável é criar uma classe CPF com um único atributo $CPF e colocar nessa clásse toda a validação e formatação para esse valor.

Dessa maneira, se o CPF for cadastrado em mais de um lugar no código, evitamos a duplicação do código relacionado ao comportamento do CPF e também evitamos valores indesejáveis nesse campo

## Exemplo

``` php
<?php

class Order
{
	public function notifyBuyer($email)
	{
	
		if (filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
			throw new InvalidEmailException;
		}
		
		return $this->repository->sendEmail($email);
	}
}
```


Nesse caso, movendo o email para uma clásse própria e centralizando todo seu comportamento nela, teremos

```php
<?php

class Email {

	public $email;
	
	public function __construct($email)
	{
		
		if (filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
			throw new InvalidEmailException;
		}
		
		return $this->email = $email;
		
	}
		
}
		
class Order{
	
	public function notifyBuyer($email)
	{
		return $this->repository->sendEmail(new Email($email));
	}
}
```

Ao aplicarmos esse conceito, podemos ver também que aplicamos o [[Single Responsibility Principle]] pois a classe order não verifica mais se o email é válido e também o conceito de [[Tell, don't ask]] pois deixamos dentro da classe toda a validação necessária para popular o campo email