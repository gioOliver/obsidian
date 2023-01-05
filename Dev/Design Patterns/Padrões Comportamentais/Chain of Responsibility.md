Também conhecido por Chain of Command, a cadeia de responsabilide consite em várias pequenas classes (Handlers) contendo apenas uma regra onde, ao receber uma requisição a classe decide se o conteúdo da requisição se aplica a sua regra ou não

Caso se aplique, a classe processa a requisição e retorna algo, se não, ela passa a requisição para a próxima classe e assim por diante.

A cadeia de responsabilidade pode ser usada tanto de maneira onde cada regra pode processar o conteudo e então passa-lo para a próxima regra quanto de maneira onde ou apenas uma regra se aplica, ou nenhuma.

A cadeia de respossabilidade é muito útil para substituir blocos de ifs em funções e, ao extrair uma regra para uma classe, possibilita também a reutilização de código

É essencial que todos os handlers implementem a mesma interface que contenha apenas o método execute. Em alguns casos pode haver o método setNext que recebe o próximo handler da cadeia. Deve-se também haver um Handler abstrato contendo o comportamento básico dos handlers

## Exemplo

- Primeiro criamos a interface que será usada por todos os handlers
``` php
interface Handler
{
    public function setNext(Handler $handler): Handler;

    public function handle(string $request): ?string;
}
```

``` php
```

``` php
```

``` php
```

``` php
```

``` php
```