Representa uma estrutura de arvore de objetos e permite trabalhar com essas estruturas como se fossem objetos separados.

É maneira é percorrer arvores de objetos de maneira recursiva sem precisar saber o conteudo de cada objeto pois todos os componetes da arvore seguirão a mesma interface onte, eles irão executar uma ação ou passar a requisição para um objeto abaixo de si na hierarquia.

## Conteúdo

- A interface: Define qual comportamento todos os objetos da árvore devem ter, normalmente só um comando `execute()`
- A folha:  Elemento da arvore que não tem nenhum sub elemento para delegar. Normalmente é onde é realmente realizado alguma ação
- O Container ou o Composite (E poderia muito bem ser chamado de galho já que árvore): Um elemento que contem sub elementos, normalmente outros GALHOS  ou folhas. Em galho não sabe se seus subelementos são galhos ou folhas, apenas passa a requisição a eles e aguarda a resposta
- O Cliente: Acessa todos os elementos da árvore através da interface.