
### docker login
Faz o login no dockerhub para que o seu docker local saiba quais imagens você tem ou não permissão
### Docker ps: 

mostra todos os containers rodando

### Docker run <nome_container>

roda um container
  
### Docker run ubuntu: 

roda uma imagem do ubuntu

bash: após rodar a imagem, abre o shell do ubuntu

-i roda no modo interativo: envia e recebe respostas do bash

-t troca de mensagens bidirecionais: 

### docker run nginx

roda a imagem nginx do dockerhub
 
-p 8080:80: redireciona o acesso da porta 8080 do computador para a porta 80 do container
acessa pelo browser usando localhost:8080

### docker run -p 8080:80 -v {pwd}/pasta/pc:pasta/container nginx
inicia o container do nginx dizendo que a porta 8080 do computador irá apontar para a porta 80 do docker E QUE tudo o que acontecer na pasta pasta/pc do computador vai acontecer na pasta/container do container

PWD: abreviação do linux que significa caminho da pasta atual
### docker exec <nome_container> <\command>

executa um comando dentro de um container, um ls -la da vida ou qualquer outro comando linux
### docker exec -it <nome_container> bash
Entra no container e pode navegar por ele. o shell.bat do devilbox
### docker build -t olivergio/nome_container:latest .
Constroi o container baseado na imagem gerada
### docker push olivergio/nome_container:latest
Sobe a imagem criada no dockerhub para que qualquer pessoa tenha acesso a ele.
### docker network ls
Lista todas as redes existentes no docker
### docker network inspect <nome_da_rede>
Lista todas as configurações de determinada rede