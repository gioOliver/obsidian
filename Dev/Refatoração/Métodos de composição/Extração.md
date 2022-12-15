Bom para funções grandes que violam principalmente o [[Single Responsibility Principle]] que possuem trechos de código que fazem coisas específicas e podem ser agrupados.

Ao realizar o método de extração, você garante que seu código possua funções com menos linhas de código, o que as tornam mais faceis de serem compreendidas, também manterm as funções mais objetivas ao seguirem o SRO.

Um ponto importante é se atentar em nomear as funções novas com nomes que descrevam bem a ação que será realizada, seguindo a regra de [[Não abreviar nomes de métodos e variáveis]]

Recomenda-se mover esses trechos para uma função só deles e então adicionar um chamado na função principal

```php
function printOwing() {
  $this->printBanner();

  // Print details.
  print("name:  " . $this->name);
  print("amount " . $this->getOutstanding());
}
```

Nesse caso, pode se mover as duas linhas de print para uma função só delas

``` php
function printOwing() {
  $this->printBanner();
  $this->printDetails($this->getOutstanding());
}

function printDetails($outstanding) {
  print("name:  " . $this->name);
  print("amount " . $outstanding);
}
```
