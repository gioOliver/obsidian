Permite através de uma interface a criação de objetos em uma superclasse onde cada subclasse possa alterar o tipo dos objetos criados/retornados.

Isso se torna possivel pois as classes que irão criar esses objetos irão apenas criar objetos que implementam a mesa interface e o cliente ira tratar os objetos através de sua interface de modo que não importe exatamente qual tipo de objeto será retornado.

## Conteúdo

- A interface do objeto criado: será obrigatória para todos os objetos que serão criados pela fábrica
- Os objetos: cada um com seu tipo e comportamento próprio mas todosImplementado a interface
- a fábrica: pode ou não ser uma classe abstrata
- as subclasses: Herdarão atributos da fábrica e usarão seus próprios objetos

