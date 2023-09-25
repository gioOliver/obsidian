Pasta compartilhada entre o computador e o container

Dessa maneira, ao se alterar os dados da pasta no container, eles são alterados no computador também e vice-versa.

É importante salvar em volumes tudo o que for ser alterado no container pois quando o container for finalizado e iniciado de novo, não serão perdidas as alterações.

Quando se cria um volume no docker, mas não se especifica a pasta local onde será armazenado os dados desse container, o docker cria uma pasta aleatória no computador e salva tudo nela. Desse jeito o volume irá funcionar, mas se você remover a imagem e rodar ela novamente, o diretório onde estavam os dados da imagem antiga irá se perder e o docker não conseguirá mais acessar