Princípio da Responsabilidade Única: Uma classe deve ter apenas um motivo para ser alterada.
Se ela é responsavel por salvar seus dados na base, ela não deverá ser responsavel por também gerar um relatório.

Essa regra se aplica não apenas para classes, métodos também devem ter apenas uma responsabilidade.

Ao se violar essa regra podemos criar classes que, de inicio, parecem mais eficiente mas, quanto mais elas crescem, mais dificil fica de se realizar alguma manutenção pois a classe/método acaba ficando cada vez mais amarrada e cada alteração pequena pode comprometer divérsas partes do código. O problema fica ainda pior sem a existencia de testes automatizados.

Complicações que o violamento dessa regra pode trazer

1. Falta de [[Coesão]]
2. Alto [[Acoplamento]]
3. Dificuldade na implementação de testes automatizados
4. Dificuldade de se reaproveitar o código

Exemplo de classe que viola o SRP

![[Pasted image 20221206123931.png]]

Apenas em uma classe há 3 responsabilidades diferentes que podem muito bem ser divididas entre
![[Pasted image 20221206124642.png]]
Dessa maneira, cada classe cuida apenas de uma responsabilidade do pedido
