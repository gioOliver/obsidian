Cria famílias de objetos relacionados mas sem especificar suas classes concretas

Uma familia de objetos relacionados seria, por exemplo uma serie de objetos que representam produtos com uma série de objetos que representam os estilos que esses produtos teriam

Por exemplo um monitor de computador, um gabinete, um teclado e um mouse, cada um desses objetos teria sua própria classe e cada um desses objetos poderiam ser no estilo gamer, office, normal ou retrô

A partir disso, se quisessemos criar um setup gamer, deveriamos instanciar todos os objetos de produtos junto com o objeto de estilo gamer

Uma fábrica abstrata trabalhia em cima dessa montagem, seria crado uma nova classe setupGamer que criaria todos os objetos com o estilo gamer. A mesma coisa teria que ser feita para um setupOffice, setuoNormal e setupRetro

## Conteúdo

- as interfaces de produtos/estilos: Tanto os produtos quanto os estilos, cada um implementará sua própria interface
- os produtos/estilos: cada um com seus próprios atributos e implementando as interfaces
- a fábrica abstrata: interface que declara métodos responsáveis por criar o setup
- as fábricas: Cada uma responsavel por criar um asérie de produtos do mesmo estilo
