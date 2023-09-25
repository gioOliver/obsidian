
- indentar com barra de espaço(dois espaços), evitar tab
- Usa hífen para fazer listas
- Usar dois pontos para separar chave: valor
- Ao indicar um valor com aspas duplar, pode se adicionar comandos como /n
- O uso do pipe | mantém a estrutura de um valor com muitas linhas
- O uso do > não mantém a estrutura das linhas, ele apresenta tudo junto na mesma linha

```YAML
host: test
datacenter:
  location: São Paulo
  router: 42
roles:
  - web
  - dns
functionamento: |
  segunda  - das 8h as 9h
  tercça   - das 9h as 11h
  quarte   - das 15h as 10h
comentarios: >
  tem uma linha aqui
  outro comentario
  é isso aí
  
    autor do comentario
    nome da pessoa
```
