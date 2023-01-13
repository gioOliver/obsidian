O driver de uma fila especifíca em qual tipo de backend ela será executada, podendo ser no serviço de filas da AWS o SQS, em uma tabela no banco de dados, no REDIS ou em qualquer driver que você achar mais bacana para rodar a sua fila

Uma lista de drivers pode ser encontrado em config/queue com configurações defaut para diversas conexões

``` PHP
<?php  
  
return [  
   
    'default' => env('QUEUE_CONNECTION', 'sync'),  
  
    'connections' => [  
  
        'sync' => [  
            'driver' => 'sync',  
        ],  
  
        'database' => [  
            'driver' => 'database',  
            'table' => env('QUEUE_TABLE', 'jobs'),  
            'queue' => 'default',  
            'retry_after' => 90,  
        ],  
  
        'beanstalkd' => [  
            'driver' => 'beanstalkd',  
            'host' => 'localhost',  
            'queue' => 'default',  
            'retry_after' => 90,  
        ],  
  
        'sqs' => [  
            'driver' => 'sqs',  
            'key' => env('SQS_KEY', 'your-public-key'),  
            'secret' => env('SQS_SECRET', 'your-secret-key'),  
            'prefix' => env('SQS_PREFIX', 'https://sqs.us-east-1.amazonaws.com/your-account-id'),  
            'queue' => env('SQS_QUEUE', 'your-queue-name'),  
            'region' => env('SQS_REGION', 'us-east-1'),  
        ],  
  
        'redis' => [  
            'driver' => 'redis',  
            'connection' => env('QUEUE_REDIS_CONNECTION', 'default'),  
            'queue' => 'default',  
            'retry_after' => 90,  
            'block_for' => null,  
        ],  
  
    ],  
  
    'failed' => [  
        'database' => env('DB_CONNECTION', 'mysql'),  
        'table' => env('QUEUE_FAILED_TABLE', 'failed_jobs'),  
    ],  
  
];

```