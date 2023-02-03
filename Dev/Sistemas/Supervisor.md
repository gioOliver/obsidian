+Supervisor é um programa já pré instalado em sistemas Linux responsavel por monitorar e rodar processos no sistema, é possivel encontrá-lo em `/etc/supervisor` ou `/etc/supervisord.d` ou algo parecido

Para ativar o supervisor, um simples `sudo supervisorctl start` já basta

Caso você queira adicionar programas para o supervisor supervisionar deve-se criar um pasta `conf.d` em `/etc/supervisord.d` com o comando `sudo mkdir /etc/supervisord.d/conf.d`

Criada a pasta conf.d, devemos editar o arquivo `supervisord.conf` com um `nano /etc/supervisord.conf` e então indo com as setas do teclado até o final do documento onde encontraremos um 

``` conf
[include]
files = supervisord.d/*.ini
```

Então substiruiremos por

``` conf
[include]
files = supervisord.d/conf.d/*.conf
```

para que o supervisor saiba onde estarão todos os arquivos de configuração.

Feito isso, é necessário criar um arquivo .conf para cada processo que você deseje que o supervisor monitore.

###Exemplo de um .conf para monitoramento de filas

`sudo nano /etc/supervisord.d/conf.d/laravel-worker.conf` - sempre se certifique de que o arquivo criado seja na extenção .conf

``` conf
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /data/www/html/pagamentos.conexaorapida.com.br/artisan queue:work --timeout=3300 --tries=3 --queue-laravel-queue
autostart=true
autorestart=true
numprocs=3
redirect_stderr=true
stdout_logfile=/data/www/html/pagamentos.conexaorapida.com.br/storage/logs/worker.log

```

com essa configuração, diremos ao supervisor que:

1. `program:laravel-worker`: 
	- O nome dessa configuração/programa será laravel-worker
2. `process_name=%(program_name)s_%(process_num)02d`
	- O nome do processo quando for dado um `php artisan queue:list` será o mesmo nome do programa, ou seja laravel-worker junto com o seu numero de processo. Caso haja configurado masi do que um worker para esse programa, resultando em `laravel-worker_00`  e `laravel-worker_01` para o caso de dois workers
3. `command`
	- o comando que o supervisor irá rodar. Nesse caso é um ativamento da fila chamada laravel-worker, com 3300 segundos de timeout e, caso de erro, retentar até 3 vezes
4. `autostart e autorestart` 
	- O programa será iniciado e reiniciado automaticamente
5. `numprocs`
	- O numero de processos/workers que serão inicializados. quanto maior o número maior a quantidade de itens da fila que irão rodar simultaneamente
6. `stdout_logfile` O caminho para salvar o log desses processos