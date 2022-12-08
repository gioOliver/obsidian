
Principio aberto-fechado define que objetos/entidades devem estar abertos para extensão e fechados para modificação.

Ótimo para funções que já dependem de muitas regras e tem tudo para depender de ainda mais regras futuramente. Conversa muito com o padrão de design [strategy](obsidian://open?vault=obsidian&file=Dev%2FDesign%20Patterns%2FPadr%C3%B5es%20Comportamentais%2FStrategy)

No geral, cada vez que o objeto tem que realizar uma ação que muda de acordo com diversas regras, no lugar de um monte de if nessa ação, deve se fazer o objeto consumir apenas uma interface e cada regra deve ter sua propria classe que implementa a interface criada. Dessa maneira cada vez que uma nova regra for adicionada ao sistema, o objeto não mudará em nada, apenas será adicionada uma nova classe com a regra.

> Alterar uma classe já existente para adicionar um novo comportamento, corremos um sério risco de introduzir bugs em algo que já estava funcionando.


# Na prática

![[Pasted image 20221208124545.png]]
Aqui temos um caso onde para calcular o salario de um colaborador, a classe FolhaDePagamento tem que fazer um if para cada tipo de contrato

Se a empresa passar a trabalhar com PJ, Cooperado, freelance, etc. um novo if deve ser adicionado a função calcular o que poder causar o mal funcionamento de funções já existentes

![[Pasted image 20221208125112.png]]

A Solução pelo OCP consiste em remover todas as verificações da FolhaDePagamento e chamar apenas a função remuneracao() que se econtra numa interface.

Cada classe de contrato estará implementando essa interface e aplicando sua própria regra para remuneracao(). Dessa maneira, ao começar a trabalhar também com PJ, é só criar uma classe de contrato PJ implementar a interface e aplicar a regra de remuneração.