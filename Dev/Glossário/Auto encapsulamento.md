Cria um método SET privado para que o constutor fique mais simples

``` php

public function __construct($valor){

	$this->setValor($valor);

}


private function setValor($valor)
{
	$valor_alterado = $valor * 0.9;
	
	//realiza validações ligadas ao valor
	//realiza outras alterações ligadas ao valor

	return $valor_alterado;
}
```
