Nos permite ter certeza de que determinada classe terá apenas uma instância em todo o processo. Permite também que o objeto possa ser acessado em qualquer lugar do código indepenente de onde e quando foi instanciado.

Para isso precisamos, em nossa classe que se tornará um singleton, primeiro deixar o construtor privado e então criar um método estático que chame o construtor da classe e salve seu conteúdo em um campo estático. Assim cada vez que esse método for chamado, ele verificará se o campo foi preenchido, se sim, retorna o campo, se não, instancia a classe, preenche o campo e então o retorna.

Esse padrão é tão simples que, ao invés de anotar o conteúdo dele, vou só deixar aqui o exemplo do refactoring guru

![[Pasted image 20230306125040.png]]