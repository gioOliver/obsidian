Permite que você tenha isole um comportamento específico de uma classe que pode ser realizado de diversas maneiras diferentes. Cada maneira de realizar esse comportamento vira uma classe de strategy que segue uma interface strategy

O padrão consiste em uma classe de contexto que irá receber e executar uma estratégia, uma interface  para estratégias, normalmente apenas com a função `execute()`, e estratégias que usam essa interface e implementem cada uma um comportamento diferente para a função `execute()`



## Exemplo


### Contexto útil

Pode muito bem ser usado para gerar parcelas de diferentes tipos de vendas

Vendas a vista geram apenas uma parcela com uma transação

Vendas parceladas no banco geram n parcelas mas com apenas uma transação

Vendas parceladas na loja geram n parcelas cada uma tendo uma transação


### Código


