Essa regra vai de encontro a tudo que aprendemos no inicio dos estudos de orientação a objetos mas também ajuda a evitar duplicação de regras/tomadas de decisões pois, ao invés de se ter getters e setters comuns na classe, podemos deixar nela toda a regra que essa classe deveria ter em suas propriedades

## Exemplo

```php
public class Jogo  
{  
    public function getScore()
	{
		return $this->score;
	}

	public function setScore( $score )
	{
		$this->score = $score;
	}
}

public class controller{

	$jogo = new Jogo();
	
	$jogo->setScore(jogo->getScore + PONTOS_INIMIGOS_DESTRUIDO);

}

```

Desse modo, é violado o [[Open-Closed Principle]] e ainda causa a possibilidade de duplicação de código cada vez que for adicionado mais pontuação pois a regra é aplicada cada vez que é adicionado mais pontos ao score

```php
public class Jogo  
{  
    protected int $score; 

    public function AdicionarScore(int $pontos)  
    {  
        this->score += $pontos;  
    }  
}

public class controller{

	$jogo = new Jogo();
	$jogo->AdicionarScore(PONTOS_INIMIGOS_DESTRUIDO);

}
```

Ao remover os getters e setters e adicionar uma função que adiciona pontos ao score, mantemos toda a regra de pontuação dentro da classe e evitamos a duplicação de código.

Até podemos implementar um método getScore simples caso ele seja necessário em alguma parte do código mas, enquanto não é necessário, podemos manter sem e seguir a vida