No geral, é ótima para tarefas que demandam muito tempo de processamento.

É recebido uma requisição e, durante o processamento, ao invés de se realizar toda a tarefa, o grosso é adicionado a uma fila, e então é retornado sucesso.

Após ser adicionado à fila, o sistema irá rodar a tarefa em background.

Para utilizar uma fila, devemos primeiro escolher e configurar o [[Driver]] que ela irá utilizar

Para salvar a fila no banco de dados, deve-se definir no env QUEUE_CONNECTION=database. Caso seja necessário mudar as configurações padrão da fila, deve mudar na pasta config/queue os da fila.

Feito isso, adicionamos toda a lógica a ser executada em uma [[Job]]

E então usamos o comando `php artisan queue:work` para acionarmos nossa fila localmente

Em casos de filas executadas no banco de dados, caso alguma das jobs dê erro, ela será adicionada na tabela `failed jobs` onde será possivel ver o motivo da exeção.

Caso o erro não tenha a ver com o código ou os parametreos da jobs, é possivel mandar todos os itens de `failed_jobs` de volta para a fila de execução com o comando `php artisan queue:retry --all`

Ou, listar as jobs com erro com ``php artisan queue:failed`` e então rodar `php artisan queue:retry {id}` param mandar uma job especifica de volta a fila de execução.

Se não for possivel enviar a job de volta para a fila, o comando `php artisan queue:forget` apaga todos os registros de falha da tabela ou `php artisan queue:forget {id}` para apagar apenas um.

Para manter as jobas rodando em produção, é necessário o uso do [[Supervisor]]
