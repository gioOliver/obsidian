Padrão que permite você criar objetos complexos passo a passo. Assim, usando o mesmo codigo, é possivel criar tipos diferentes de representação de um objeto.

Muito útil para objetos gigantes que, em seu construtor iriam muitos parâmetros e acabaria com uma chamda de classe enorme e feia

O rolê do Builder é extrair os parametros do construtor da classe gigante e colocá-los em suas próprias classes com seus próprios atributos. Dessa forma, cada pequena classe, representa um passo a ser ultilizado pelo Builder, e dependendo dos parâmetros de cada classe, o resultado final pode dar diversos objetos diferentes com mais ou menos passos.

Pode ser útil no caso de criação de uma venda pois a venda além dos seus parâmetros normais, pode ter split, itens, link, cliente, paciente, nota fiscal e muito mais coisa.

Além do builder, podemos também criar uma classe Diretor que será responsável por instanciar todas as classes que irão formar o builder. Isso não é obrigatório no padrão pois pode ser feito direto do client code

## Conteúdo

- A inteface do builder: declara todos os passos necessário para se construir um produto
- O builder: Responsável por implementar todos os passos e gerar classes produto
- As classes produto: Resultado do builder, não é necessário que elas sigam a mesma hierarquia ou interface
- O diretor: Opcional, contém vários métodos que geram produtos diferentes.
