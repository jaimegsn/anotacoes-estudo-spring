# Spring Security

O Spring Security é um framework de segurança poderoso para aplicações Java, imagine uma situação em que lidamos com uma aplicação contendo dados confidenciais, como transações financeiras, é absolutamente essencial assegurar que os usuários não possam executar ações indiscriminadamente, a qualquer momento, ou acessar operações não autorizadas.

Nesse contexto, o Spring Security se destaca ao oferecer uma solução para implementar medidas de segurança eficazes, ele permite a autenticação, bem como a autorização, você pode configurar regras de acesso granulares, definindo quem pode acessar quais partes da aplicação e quais operações estão disponíveis para eles.

### Dependência:

pom.xml:

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-security</artifactId>
</dependency>

<!-- https://mvnrepository.com/artifact/com.auth0/java-jwt -->
<dependency>
	<groupId>com.auth0</groupId>
	<artifactId>java-jwt</artifactId>
	<version>4.4.0</version>
</dependency>
```