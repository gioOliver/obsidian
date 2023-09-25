- Usada para armazenar e reutilizar dados

É definida pelo sinal de `&nome` onde, tudo o que vem depois dele será o valor da ancora

Para usar o valor em outros lugares, basta chamar com `*nome`


``` YAML
host: test
datacenter:
  location: &SP São Paulo
  router: 42
roles: &basicRoles
  - web
  - dns
---
host: other
datacenter:
  location: *SP
  router: 44
roles: *basicRoles
```