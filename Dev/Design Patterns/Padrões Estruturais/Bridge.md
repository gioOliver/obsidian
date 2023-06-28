Padrão de design que divide uma classe grande ou várias pequenas mas parecidas e relacionadas entre [[Abstração]] e [[Implementação]] que podem ser desenvolvidas de maneira independente.

No caso, ele dividiria uma herança de classe que cresce o número de subclasses descontroladamente em mais de uma herança

Exemplo, a classe formaGeometrica tem as subclasses redondo e quadrado. Se for necessario adicionar cor às formas, acabaremos tendo subclasses quadadoAzul, quadradoVermelho, redondoAzul e redondoVermelho o que pode acabar crescendo descontroladamente.

Para resolver isso, criamos duas heranças diferente e usamos a também composição de classe ao invés de apenas herança. No final teremos Forma com subclasses quadrado e redondo e Cor com subclasses Vermelho e Azul, feito isso é só dizer que Forma possui Cor e show de bola.


## Conteúdo

 - Abstração: onde fica todo o controle e todas as chamadas de métodos. Não funciona sem as classes de implementação
 - As subclasses da Abstração: possuem comportamentos mais especifico
- A inteface da implemntação: Uma regular interface que vai listar todos os métodos que terá na implementação.
- As classes de implementação: Onde vai ficar toda a regra de negócio
