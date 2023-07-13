
Como se fosse uma planta baixa de um prédio 

Nela é indicado tudo o que o container deve ter como versão de php por exemplo

## Criando uma imagem

Primeiro de tudo, deve se criar um arquivo chamado `dockerfile` 

Nesse arquivo, dizemos qual imagem do dockerhub queremos nos basear

```` dockerfile
#sempre partimos de alguma imagem
FROM nginx:latest

#ao rodar o container, será copiado o arquivo index.html do meu computador para a pasta html do container
COPY html/index.html /usr/share/html/

```