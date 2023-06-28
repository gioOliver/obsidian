Permite copiar objetos sem depender do funcionamento interno deles. Realiza uma cópia completa do objeto independente de o objeto ter ou não atributos privados ou ser acessado via interface. Desse jeito diminui o possível [[Acoplamento]] que ocorreria com o objeto a ser clonado.

Para isso é criado uma inteface `clonavel` que terá apenas o método `clone()` e fazer com que as classes implemente essa interface. Após isso, basta implementar o método fazendo com que o objeto novo receba todos os atribubos do antigo. Ao fazer isso de dentro da classe, é possivel acessar até os atributos privados, e assim, realizar a cópia exata do objeto.

As classes que implementarem a interface, serão as classes protótipos.

## Conteúdo

- A interface: Contém apenas o método `clone()` e é implementada por toda classe que for ter essa função.
- A classe protótipo: Contém o método `clone()` da interface e é responsavel por criar um novo objeto igual a sí. Dentro do método também pode ter alguma alteração em um ou outro atributo do objeto clonado antes de retornar.