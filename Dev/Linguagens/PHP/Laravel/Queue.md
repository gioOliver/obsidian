No geral, é ótima para tarefas que demandam muito tempo de processamento.

É recebido uma requisição, durante o processamento, ao invés de se realizar toda a tarefa, o grosso é adicionado a uma fila, e então é retornado sucesso.

Após ser adicionado à fila, o sistema irá rodar a tarefa em background.

Para salvar a fila no banco de dados, deve-se definir no env QUEUE_DRIVER=database. Caso seja necessário mudar as configurações padrão da fila, deve mudar na pasta config/queue os da fila.

Deverá também ser adicionano no banco de dados a tabela jobs e failed_jobs. Esses nomes são padrão do Laravel mas pode ser alterado em cofigs/jobs

## Jobs

Classe onde será executado todo o processo de uma tarefa colocada na fila

Normalmente tem apenas a classe handle() que é onde toda a magia acontece, mas pode também ter um constructor para receber parametros.



