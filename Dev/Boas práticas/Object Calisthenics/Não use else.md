Uma regra um pouco estranha quando vista pela primeira vez, mas que quanto mais se usa, menos se vê a necessidade do else

O else, no geral costuma trazer mais complexidade para o código, o que dificulta a leitura

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

