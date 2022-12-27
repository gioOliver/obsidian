Além de dificultar a leitura de um código, a abreviação de nomes de métodos pode indicar um problema maior como uma violação do [[Single Responsibility Principle]] pois o método pode estar fazendo alguma ação a mais do que ele deveria

Em caso de váriaveis, é normal encontrarmos uma variável $i para um index/contador e, por mais que isso pareça pequeno, abre caminho para outras letras como $k e $v para Key e Value e muitas outras que irão dificultar cada vez mais a leitura do código

O ideal é que nomes de classes e variáveis tenham no máximo duas palavras e que sejam o mais descritivos o possível


## Ex

Se tivermos um classe ``Profile`` e um método nessa classe que crie um perfil, o método deverá se chamar apenas ``Create`` e não ``CreateProfile`` pois o método será chamado ``$profile->create()``, dessa forma se evita redundância e sabemos exatamente o que o método faz.