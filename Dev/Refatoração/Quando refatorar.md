Quando refatorar?

O ideal é seguir a regra do terceiro

> 1.  Quando você estiver fazendo algo pela primeira vez, faça-o.
	2.  Quando você estiver fazendo algo semelhante pela segunda vez, recue por ter que repetir, mas faça a mesma coisa de qualquer maneira.
	3.  Quando você estiver fazendo algo pela terceira vez, comece a refatorar.

Também podemos refatorar quando estamos adicionando uma nova funcionalidade ao código. Sempre que se lê o trecho de código onde será inserida a nova funcionalidade, deve-se também procurar por resquicios de código sujo e refarorá-los pois, a próxima pessoa que passar por lá, não terá a dificuldade que você teve.

O mesmo vale para quando for feita alguma correção de bug, se há sujeira por volta do bug, limpe tudo para que não ocorra outros bugs no futuro

## Como refatorar

O objetivo de refatorar um código é pegar algo que funciona, mudar seu interior e manter funcionando do mesmo jeito do que antes só que melhor. Para isso, devemos nos atentar a alguns pontos:

### 1. O código deve ficar mais limpo
	- Se você refatorou um trecho e, mesmo assim, ele ainda tem sujeira, você não refatorou direito e isso vai causar trabalho no futuro
	- Se o código estiver no ponto onde qualquer refatoração causa mais sujeira ainda, deve-se considerar reescrever todo o trecho de código de uma maneira organizada. Para isso, certifique-se de esse trecho esteja com a maior cobertura de testes o possível

### 2. Novas funcionalidades não deverão ser feitas
	- Não misture as coisas, refatore primeiro, commite e depois adicione a nova funcionalidade.

### 3. Todos os testes devem passar após a refatoração
	- O sistema tem que funcionar exatamente da mesma maneira do que funcionava antes