# Documentação da API com Swagger

Com o Swagger, é possível criar uma documentação interativa e amigável para suas APIs, permitindo que outros desenvolvedores entendam rapidamente como interagir com os endpoints e quais parâmetros e respostas esperar. Essa documentação é gerada automaticamente a partir da descrição da API, que é feita usando a especificação OpenAPI.

**A especificação OpenAPI** é escrita em formato YAML ou JSON e descreve detalhadamente cada endpoint da API, incluindo os parâmetros, tipos de dados, métodos HTTP aceitos, códigos de status, modelos de dados de entrada e saída, entre outros aspectos.

Além da documentação, o Swagger também fornece uma interface gráfica interativa, conhecida como Swagger UI, que permite aos desenvolvedores testar e explorar a API sem a necessidade de escrever código manualmente. Isso torna o desenvolvimento e o consumo de APIs muito mais eficientes e eficazes.

Podemos acessar a documentação por esses dois links:

- http://localhost:8080/v3/api-docs

- http://localhost:8080/swagger-ui/index.html

O V3 é a versão do swagger e não da nossa API

### Dependência:

Link: https://mvnrepository.com/artifact/org.springdoc/springdoc-openapi-starter-webmvc-ui, **pegar a versão mais recente e estável**

```xml
<!-- https://mvnrepository.com/artifact/org.springdoc/springdoc-openapi-starter-webmvc-ui -->
		<dependency>
			<groupId>org.springdoc</groupId>
			<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
			<version>2.1.0</version>
		</dependency>
```

### Configuração Básica do Swagger:

Criaremos essa classe de configuração:

```java
@Configuration
public class OpenAPIConfig {

    @Bean
    public OpenAPI customOpenAPI () {
        return new OpenAPI().info(new Info()
                .title("RESTful API with Java 17 and Spring Boot 3")
                .version("v1")
                .description("Some description about your API")
                .termsOfService("Any link for terms of service")
                .license(
                        new License()
                                .name("Apache 2.0")
                                .url("Any link for license")));
    }
}
```
