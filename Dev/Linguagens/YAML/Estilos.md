
### Block

Mais fácil de ler, melhor estruturado e menos compacto


```YAML
host: test
datacenter:
  location: São Paulo
  router: 42
roles:
  - web
  - dns
```


### Flow

Extensão do formato json, quebra longas lindas de conteudo e pode fazer uso de tags e ancoras

```YAML
host: "test"
datacenter: {
	location: São Paulo
	router: 42
}
roles: [web, dns]
```