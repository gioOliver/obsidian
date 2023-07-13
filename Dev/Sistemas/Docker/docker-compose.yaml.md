Responsável por rodar e configurar várias imagens de uma só vez para que tenhamos um ambiente completo de desenvolvimento com apenas um comando


``` yaml
#o número da versão que irá rodar
version: 3

#a lista de imagens que ele irá rodar
services:
	#nome do serviço no dockerhub
	mysql:
		#nome da imagem no dockerhub
		image:mysql: 8
		container_name: mysql
		#sempre que der problema, reinicia o container
		restart: always
		#vairaveis de ambiente
		enviroment:
			MYSQL_ROOT_PASSWORD: root
			MYSQL_DATABASE: nome_do_banco
			MYSQL_USER: root
		#portas mapeadas do computador para o container
		ports:
			- 3306:3306
		#garante que sempre que reiniciado o container, o banco de dados não será perdido pois está compatilhado em uma pasta no computador
		volumes:
			- ./mysql:var/lib/mysql


```

e para rodar ele, basta dar um `docker compose up -d`