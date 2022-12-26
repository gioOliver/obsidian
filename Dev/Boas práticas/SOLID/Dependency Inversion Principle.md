Princípio de inversão de dependência: Dependa de abstrações e não de implementações

>1 - [[Módulo de Alto Nível]] não deve depender e [[módulo de baixo nível]]. Ambos devem depender de abstrações
> 2- Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações"

Ou seja, tudo deve depender de abstrações, quanto mais bem abstraído, melhor

Agora o que é uma abstração???

Nesse caso, interfaces. O ideal é que a programação quando orientada a objeto seja sempre focada em interfaces.

Outro ponto importante. Esse conceito do [[SOLID]] é relacionado a inversão de dependências, não [[Dependency Injection]], apesar de a injeção de dependência ser muito usada nesse conceito.

### Exemplo


![[Pasted image 20221213210008 1.png]]

Só nesse trecho de código já podemos ver que há um alto nível de [[Acoplamento]] pois para usar a classe, deve-se obrogatoriamente instanciar o MySQLConnection.


![[Pasted image 20221213210209 1.png]]

Uma das saídas seria justamente utilizar a Injeção de dependência. Assim, a classe já vem instanciada. Mas, mesmo assim, ainda não está bom o suficiente pois ainda estamos violando o DIP e, além disso, estamos violando o [[Open-Closed Principle]] pois, se quisermos usar a mesma classe com um banco de dados Oracle, não seria possível pois seria necessário editar a classe ao invés de extendê-la.

![[Pasted image 20221213210647 1.png]]

Então, para resolver de vez o problema, usamos ela, a maravilhosa e abstrata, interface.

É criada uma interface DBConnection e, cada classe de banco de dados implementa os métodos dela.

A partir disso, na classe PasswordReminder, passamos a depender da interface DBConnection e, não fazemos ideia de qual banco de dados está sendo usado a classe, só sabemos que ela vai funcionar, seja com um banco de dados, seja com mil, se todos implementarem a interface, sucesso.