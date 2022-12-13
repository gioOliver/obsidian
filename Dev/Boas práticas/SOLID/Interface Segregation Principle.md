Princípio de Segregação de Interfaces: Uma classe não pode ser forçada a implementar interfaces e métodos que não irá utilizar

No geral, se uma classe vai implementar uma interface e, nessa interface, há um ou mais métodos que a clásse não irá utilizar, vale mais a pena não implementar essa interface e criar uma outra interface para a classe apenas com os métodos que ela utilizará

![[Pasted image 20221212204751.png]]![[Pasted image 20221212204812.png]]

Pode se ver nesse exemplo que pinguim está implementando a interface aves, mas em aves há o atributo setAltitude, que não faz sentido para um pinguim já que ele não voa. Assim o método setAltitude de pinguim será um método vazio vilando tanto o ISP quanto o [[Liskov Substitution Principle]]

![[Pasted image 20221212205038.png]]
![[Pasted image 20221212205050.png]]

A soplução nesse caso foi remover o set altitude de aves e criar uma nova interface avesQueVoam que extende aves.

Dessa maneira pinguim pode tranquilamente implementar a interface aves com todos seu métodos assim como avestruz e dodô(que deus os tenha) enquanta os passarinhos, pombos e o papacu de cabeça roxa implementam a interface avesQueVoam que vai ter tanto métodos de aves voadoras quanto o de aves no geral