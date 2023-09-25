Pode se ter múltiplas diretivas/configurações em um mesmo arquivo

Para isso usa-se o `---`

```YAML
host: test
datacenter:
  location: São Paulo
  router: 42
roles:
  - web
  - dns
---
host: test2
datacenter:
  location: São Paulo
  router: 422
roles:
  - web
  - dns
---

host: test3
datacenter:
  location: São Paulo
  router: 44
roles:
  - web
  - dns
```

