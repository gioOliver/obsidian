Um dos conceitos mais complicados a primeira vista de se por em prática, mas, ao se adicionar no dia a dia, podemos ver códigos mais limpos e mais legíveis

Normalmente, apenas aplicando o conceito de [[Fail fast]] e [[Early Return]], já é possível acabar com quase todos os `else` do código

Em casos mais complexos, pode ser necessário aplicar algum padrão de design como o [[State]] ou o [[Strategy]]

## Exemplo

``` php
<?php

protected function indexAction()
{
	
	if ($this->security->isGranted('ADMIN')) {		
		$view = 'admin/index.html.twig';
	} else {
		$view = 'home/access_denied.html.twig';
	}
	
	return $this->render($view);

}
```

Nesse caso, podemos remover o else apenas com um early return

``` php
<?php

protected function indexAction()
{
	if ($this->security->isGranted('ADMIN')) {
		return $this->render('admin/index.html.twig');
	}

	return $this->render('home/access_denied.html.twig');
}
```