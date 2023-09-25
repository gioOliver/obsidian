É um arquivo .yaml onde ficam todas as instruções para o sistema buildar um ou mais containers

``` YAML
# Normalmente é o comando inicial de um dockerfile, ele indica qual imagem vai ser o ponto inicial que nossa imagem irá usar. Nesse caso a imagem será construida a partir a versão 1.19.4 do NGINX
FROM nginx:1.19.4-alpine
# Nome e contato de quem criou/mantém a imagem
LABEL maintener="Giovaani <gio.oliver.97@gmail.com>"
# Faz uma cópia de todos os arquivos da pasta onde se encontra o dockerfile para a pasta dentro do container, normalmente é nessa pasta onde estarão os volumes criados
COPY . /usr/share/nginx/html
# Qual porta o docker deve expor para espelhar com uma porta da nossa máquina 
EXPOSE 80
# Diretório onde a aplicação estará rodando
WORKDIR /usr/share/nginx/html
# Comando para rodar comando após configrar o container, pode se concatenar comandos com o &&, quando se usa uma versão alpine, se usa o APK ao invés de APT
RUN apk update && apk zlib-dev jpeg-dev && php artisan migrate 
# Comando executado no workdir assim que o container for criado, normalmente algum comando para iniciar a aplicação
ENTRYPOINT php artisan serve --host 127.0.0.1 --port 8080
# Porta que será exposta a aplicação
EXPOSE 8080
```

Para rodar, bastar dar o comando

`docker build -f Dockerfile -t giooliver/servidor_web:v1`

docker build: Comando para o docker buildar a partir de um arquivo
-f Dockerfile: indicação do nome do arquivo com os comandos, se o arquivo se chamar Dockerfile, não é necessário especificar
-t giooliver/servidor_web:v1: Indica a criação de uma tag, onde giooliver deve ser o user do dockerhub de quem está criando o dockerfile. /servidor_web é o nome da tag que será criada e :v1 é a versão atual da tag

