Utilizadas para configurar uma uri/url prória, um marcador local ou um tipo de dado


```YAML
%TAG ! tag:host:geek:
---
host: test
datacenter:
  location: !GEEK São Paulo
  router: 42
roles:
  - web
  - dns
---
host: test
datacenter:
  location: São Paulo
  router: !!str 42
  switch: !!str 42
roles:
  - web
  - dns
```