# Criando um projeto com Spring Initializr

Para criarmos um projeto Spring Boot precisamos ir ao site do [Spring Initializr](https://start.spring.io/)

Onde nele:

1. Selecionamos nosso gerenciador de dependências: maven ou gradle
2. Linguagem: java, kotlin ou groove
3. Versão do spring (escolher a mais recente sem ser SNAPSHOOT)
4. Group é normalmente o nome da empresa, instituição… : com.empresax
5. Artifact é normalmente o nome do projeto: nomeprojeto
6. Packaging é o formato de como as dependências vão ficar, por padrão escolho jar
7. Depois a versão do JAVA
8. E por último no canto direito inserimos as dependências iniciais do nosso projeto: Spring Web, Spring Data JPA, Lombok…. que essas dependências já vão vir configuradas no gerenciador de dependências (maven ou gradle)
   1. Spring Web, para que o nosso projeto seja um projeto básico de spring para web
   2. Lombok através de annotations evita com que tenhamos que escrever operações trabalhosas e repetitivas como getters e setters, consturtores e etc.
9. Após tudo isso clicamos em generate que irá nos gerar um arquivo ZIP.

## Alguns Exemplos de Dependências do Spring Initializr:

As dependências fornecidas pelo Spring Initializr são componentes de software que são incorporados ao projeto para fornecer recursos e funcionalidades adicionais.

- **Spring Web:** Essa dependência permite a criação de aplicativos da web com o Spring MVC. Ela fornece recursos para criar controladores, lidar com solicitações HTTP, gerenciar rotas, etc.
- **Spring Boot DevTools:** Essa dependência facilita o desenvolvimento de aplicativos Spring Boot, fornecendo recursos de desenvolvimento, como a reinicialização automática (hot swap). Isso permite atualizar o código-fonte do projeto em tempo de execução, refletindo as alterações sem a necessidade de reiniciar manualmente o servidor.
- **Spring Data JPA:** Essa dependência simplifica o acesso e a manipulação de dados em um banco de dados relacional com o uso do padrão JPA (Java Persistence API). Ela fornece recursos para criar repositórios e realizar operações CRUD (Create, Read, Update, Delete) de forma mais fácil e eficiente.
- **PostgreSQL Driver:** Essa dependência é o driver JDBC para o PostgreSQL, permitindo a conexão e interação com bancos de dados PostgreSQL em um aplicativo Java. Ela fornece os meios necessários para se comunicar com o banco de dados e executar consultas e operações.
- **MySQL Driver:** Essa dependência é o driver JDBC para o MySQL, permitindo a conexão e interação com bancos de dados MySQL em um aplicativo Java. Assim como o PostgreSQL Driver, ela fornece os meios necessários para se comunicar com o banco de dados e executar consultas e operações.
