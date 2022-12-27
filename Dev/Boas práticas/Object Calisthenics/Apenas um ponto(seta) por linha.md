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

	public function getTransacao()
	{
		return $this->transacao;
	}
}

class Venda
{
	private $parcela;

	public function getDataTransacao()
	{
		return $this->parcela->transacao->getDataTransacao;
	}
}
```