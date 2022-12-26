Se a sua classe possui um atributo que seja um array/uma estrutura de dados, ela deve ser extraida para uma classe onde ela seja o único atributo. Dessa forma, esse arrya pode ser tipado e manipulado do jeito certo e tendo todos os seu métodos específicos agrupados em sua própria classe/coleção.

```php

class ListaCompras{

	protected string $categoria;
	protected array $produtos;

}

```

Nesse caso, temos um array de produtos em uma lista de compras, porém, é apenas um array comum. Poderiamos preencher ele tanto com 

```php

$produtos = [
	[
		'nome' => 'café'
		'valor' => '14,60'
	],
	[
		'nome' => 'Arroz'
		'valor' => '4,99'
	]
]

```

Quanto com

```php
$produtos = ['café', 'tomate', 'manga'];
```

O que poderia causar comportamentos inesperados no nosso código e enxer ele de bugs.

Para resolver isso, aplicamos a regra First Class Collections ou coleções de primeira classe

```php
class Produto{

	private string $nome;
	private float $valor;
	
	__construct( string $nome, float $valor){
		$this->nome = $nome;
		$this->valor = $valor;
	}
}

class ListaProdutos{
	
	private array produtos;

	public add(Produto $produto)
	{
		$this->produtos[] = $produto;
	}

	public list()
	{
		return $this->produtos;
	}

}

class ListaCompras{

	private string $categoria;
	private Produto $produto;

	public function setProduto( Produto $produto){
		$this->produto = $produto;
	}

}
```

Desse modo, consiguimos aplicar o [[Single Responsibility Principle]] e ainda aplicar as [[Collection]]s criando uma classe própria para as propriedades de produto, uma collection para agrupar todos os produtos e depois apenas adicionarmos essa colection como um atributo da Lista de comparas. Assim, cada propriedade pode gerenciar seus próprios comportamentos e no final não teremos resultados inesperados independente de onde e quantas vezes a classe ListaCompras seja usada.