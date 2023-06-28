Classe onde será executado todo o processo de uma tarefa colocada na fila

Normalmente tem apenas a classe handle() que é onde toda a magia acontece, mas pode também ter um constructor para receber parametros.

Recommendado nesse caso extrair toda a lógica de uma job para um [[Command]] e então apenas chamar sua execução