Também conhecida com Lei de Demeter, ou Don't talk to strangers diz que uma classe deve se comunicar apenas com classes diretamente ligadas a elas e não com classes terceiras

```php
class Transacao
{
	private data_transacao;

	public function getDataTransacao()
	{
		return $this->data_transacao;
	}
}


class Parcela
{
	private Transacao $transacao;

	public function getDataTransacao()
	{
		$this->transacao->getDataTransacao()
	}
}

class Venda
{
	private $parcela;

	public function getDataTransacao()
	{
		return $this->parcela->getDataTransacao;
	}
}
```

Em casos de classe que se autoreferrenciam, não há motivos para seguir a risca o "apenas um ponto/seta" mas é importante que a classe acesse atributos e métodos apenas de classes ligadas diretamente a ela, ou seja, apenas dois pontos/setas por linha