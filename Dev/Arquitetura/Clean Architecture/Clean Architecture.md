
Segue conceitos de Clean Code e implementa o [[SOLID]]. Foca em manter a logica de negócio, ou o domínio da aplicação, isolado, evitando alto [[Acoplamento]], facilitando a escrita de testes automatizados, alterações em diferentes camadas ou o crescimento do código.

É representada pelo segunte diagrama:

![[Pasted image 20230327121836.png]]

Como o diagrama mostra, o fluxo da aplicação é sempre das camadas externas para as camadas internas de modo que, uma camada não pode ter acesso a camadas exteriores, apenas interiores.

As 4 camadas do diagrama:
 1. [Entidades / Regras de negócio](Entidades)
 2. [Casos de uso / Regras de aplicação](obsidian://open?vault=obsidian&file=Dev%2FArquitetura%2FClean%20Architecture%2FCasos%20de%20Uso)
 4. Adaptadores de interface
 5. Framework e Drivers