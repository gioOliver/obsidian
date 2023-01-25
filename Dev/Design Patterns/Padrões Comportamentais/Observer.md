Também conhecido por Listener, esse padrão é responsável por notificar um ou mais objetos quando ocorrer qualquer alteração no objeto que está sendo observado/ouvido.

Pode se classificar o objeto observado com um publisher e os objetos que o observam seriam os assinantes.

O objeto publisher, deverá ter um array que guardará todo os objetos que o assinam e implementar uma interface que tenha um método para adicionar um assinante, outro para remover um assinante e um método responsável por notificar todos os assinantes.

Os assinantes por sua vez, terão que implementar uma interface que tenha um método para receber as notificações do publisher.

