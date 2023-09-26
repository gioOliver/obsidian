Arquivo YAML que concentra todas as informações necessárias para que os containers sejam criados da maneira e na ordem correta. Dessa maneira não é necessário digitar um monte de comando para buildar e rodar containers do docker, o que evita erros de digitação e retrabalho

Antigamente,no LInux, era baixado junto com o docker mas isso não ocorre mais depois da chegada do Kubernets que é um gerenciador mais poderoso de containers



``` YAML
#Versão do docker-compose a ser utilizada
version: "3.8"

# Todos os serviços que irão rodar com o docker
services:
	#serviço
	nginx:
		# Configuracao de montagem da imagem
		build: 
			#localização do dockerfile referente ao serviço
			dockerfile: ./docker/nginx.dockerfile
			#Onde será buildada a imagem
			context: .
		#D eonse será baixada a imagem
		image: giooliver/nginx_do_gio:v1
		#como será identificada a imagem
		container_name: nginx
		# Portas que o serviço irá usar
		ports:
			# Porta do meu computador:Porta do Nginx
			- "8080:80"
		# Rede específica onde o serviço irá rodar
		networks:
			- nwdogio
		# Serviços que deverão ser inicializados antes que o nginx
		depends_on:
			- appGio1
			- appGio2
			- appGio3

	pggio:
		build:
			dockerfile: ./docker/pg.dockerfile
			context: .
		image: giooliver/pggio:v1
		container_name: pggio
		ports:
			# Não há ligação entre uma porta do pc e a porta do container pois o banco de dados não é aberto para conexões externas
			- "5432"
		networks:
			- nwdogio
		volume:
			#Local de armazenamneto do volume do banco de dados
			- pgdata:/var/lib/postgresql/data

	appGio1:
		build:
			dockerfile: ./docker/appgio.dockerfile
			context: .
		image: giooliver/appgio:v1
		container_name: appgio1
		ports:
			- "8000"
		networks:
			- nwdogio
		depends_on:
			- pggio
	
	appGio2:
		build:
			dockerfile: ./docker/appgio.dockerfile
			context: .
		image: giooliver/appgio:v1
		container_name: appgio2
		ports:
			- "8000"
		networks:
			- nwdogio
		depends_on:
			- pggio
	
	appGio3:
		build:
			dockerfile: ./docker/appgio.dockerfile
			context: .
		image: giooliver/appgio:v1
		container_name: appgio3
		ports:
			- "8000"
		networks:
			- nwdogio
		depends_on:
			- pggio

# Todas as networks que serão usadas pelos containers deverão ser listadas aqui para que o docker funcione. Se não for especificada uma network, todo o container vai ser criado num range padrão de rede do docker(172.168.0.1). Dessa maneira, cada projeto docker terá seu range específico o que evita conflitos com outros sistemas no mesmo pc
networks:
	nwdogio:
		driver: bridge
		
# O mesmo serve para os volumes
volumes:
	pgdata:
```

após configurar tudo, é só rodar um `docker-compose build`para baixar tudo o que tem para baixar e, configurar as imagens.


Dando tudo certo, manda um `docker-compose up -d` e aí é só correr por abraço