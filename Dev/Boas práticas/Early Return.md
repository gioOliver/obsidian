
Um pouco parecido com o conceito [[Fail fast]], no ealy return buscamos retornar e finalizar a função o mais breve o possível, evitando assim que ela passe por validações e ações desnecessárias.

Ao aplicar esse método, podemos previnir bugs, faliciltar a manutenção e ainda deixamos o código mais legível e com melhor performance.

## Exemplo

``` php
public static function formatDate($date)  
{  
    $format = DateTime::ATOM;  
    
    if ($date instanceof DateTime) {  
        $d = $date->format($format);  
    } elseif (is_numeric($date)) {  
        $d = date($format, $date);  
    } else {  
        $d = (string) $date;  
    }  
    
    return $d;  
}
```

Podemos ver que além de violar o conceito de [[Não use else]], se a condição for verdadeira logo na primeira verificação, ela terá que passar pelas outras verificações mesmo assim, diminuido a performance do código

``` php
public static function formatDate($date)  
{  
    $format = DateTime::ATOM;  
  
    if ($date instanceof DateTime) {  
        return $date->format($format);  
    }  
  
    if (is_numeric($date)) {  
        return date($format, $date);  
    }  
  
    return (string) $date;  
}
```

Ao remover os `else` e `else if` , trocá-los por `if` e aplicar o early return, temos um código mais performático e legível.