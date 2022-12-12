
Princípio de substituição de Liskov: Uma classe filha deve ser substituível por sua classe mãe.

Ou seja, um sistema não deve mudar seu comportamento quando chamamos uma função que existe na classe mãe e na classe filha

Se o método getNome da classe mãe retorna uma string, o método getNome da classe filha deverá retornar também uma string

Se o método setValor da classe mãe recebe um valor do tipo numerico(10,2) o setValor da classe filha deve recever também um valor numérico(10,2).

As entradas e saídas dos métodos devem se manter, o que pode alterar é o processamento dos dados.

O LSV é muitas vezes utilizado com o princípio de injeção de dependências, com o [[Open-Closed Principle]] ou com o Princípio de segregação de interface.

Ao usar o LSP bonitinho, podemos ter mais confiança ao usar o [[polimorfismo]] pois chamaremos às classes filhas e mães sem nos preocuparmos com comportamentos diferentes.

## Exemplos de violação do princípio

- Sobrescrever/implementar um método que não faz nada
- Lançar uma exeção inesperada
- Retornar valores de tipos diferentes da classe base
![[Pasted image 20221212123949.png]]![[Pasted image 20221212124003.png]]