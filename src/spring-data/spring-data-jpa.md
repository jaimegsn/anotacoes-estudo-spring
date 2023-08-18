# Spring Data JPA

Bom antes das ferramentas de mapeamento-ojeto-relacional (ORM) existia uma dificuldade em se trabalhar com bancos de dados relacionais e Java pois as duas tecnologias utilizam paradigmas diferentes, uma é orientado a objetos enquanto e a outra é relacional.

Então quando iamos consultar no banco de dados alguma entidade, como por exemplo `usuario`, tinhamos que traduzir o que vinha da tabela usuário do banco em um objeto usuário no Java, percorrendo todos os dados da tabela com JDBC, além de outras dificuldades.

## JPA

Então surgiram as ferramentas de mapeamento-objeto-relacional (ORM) que tem como finalidade melhorar a comunicação de um sistema orientado a objetos e um banco de dados relacional.

Exemplo de uma ferramenta mapeamento-objeto-relacional(ORM):

JPA (Java Persistence API) é uma especificação da plataforma Java EE para gerenciamento de dados no banco de dados relacional.

O JPA é uma especificação que define uma API padrão para persistência de dados em aplicações Java. Ele foi projetado para facilitar o desenvolvimento de aplicativos que acessam bancos de dados relacionais. O JPA oferece um conjunto de anotações que podem ser usadas para mapear objetos Java para tabelas em um banco de dados relacional.

## Hibernate

Como o JPA é uma especificação(Interface) precisamos de algo que implemente ele (ex: Hibernate):

O Hibernate é uma implementação dessa especificação JPA e é uma das ferramentas mais utilizadas para gerenciamento de dados em aplicações Java.

O Hibernate é uma ferramenta ORM (Object-Relational Mapping) que permite mapear objetos Java para tabelas em um banco de dados relacional. Ele fornece um conjunto de APIs para executar operações de CRUD (Create, Read, Update e Delete) e suporta consultas em HQL (Hibernate Query Language), que é uma linguagem de consulta orientada a objetos.
