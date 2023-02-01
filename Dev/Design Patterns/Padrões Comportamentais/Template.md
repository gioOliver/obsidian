Padrão que divide um processo em diversos passos em uma classe principal junto com uma função responsável por seguir todoso os passos em ordem e permite que subclasses alterem o comportamento de um ou mais passos mas não da ordem em si

Dessa forma teremos uma superclasse com diversas funções abstratas contendo ou não um comportamento padrão e uma função responsavel por chamar cada uma delas em ordem

E teremos também diversas subclasses que irão alterar o comportamento de alguns passos de acordo com a necessidade de cada uma

Muito útil em caso de classes que tem quase o mesmo algoritimo mas com pequenas alterações
