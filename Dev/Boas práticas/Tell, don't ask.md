- Não verificar o estado de um objeto em um controller/service, apenas manda ele executar uma ação

- Ao invés de ter o if no controller, o if passa a ficar dentro do próprio objeto, garantindo que a verificação de estado seja feita apenas uma única vez


Na pretica substitui

controller
	if( $obj->estado = 1)
		$obj->executaAcao();


por 

controler
	$obj->executaAcao();

Obj
	acao()
		if( $this->estado = 1 )
			executa acao;