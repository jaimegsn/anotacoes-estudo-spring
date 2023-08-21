# Implementando o CORS de forma Global

O que vamos fazer aqui primeiramente é criar uma propriedade no application.properties ou application.yml onde essa propriedade irá receber as origens permitidas para acessas as operações. Exemplo:

```yaml
# application.properties:
cors.originPatters: http://localhost:3000,http://localhost:8080

#application.yml:
cors:
  originPatters: http://localhost:3000,http://localhost:8080
```

Essa configuração feita no application normalmente não está sendo usada em lugar algum, é algo que criamos, então precisamos chamar ela e utilizar, para fazer isso e capturar seus valores utilizaremos uma annotation chamada **`@Value`** e com isso settar o seu valor em uma variável em alguma classe, considerando nosso propósito utilizaremos uma classe de configuração. Exemplo:

```java
@Configuration
public class WebConfig implements WebMvcConfigurer{
	@Value("${cors.originPatterns:default}")
    private String corsOriginPatterns = "";
}
```

O **‘default’** significa que caso não seja encontrada um valor para nessa configuração no application.properties será assumido o valor que estiver na variável **`corsOriginPatterns`**

A classe de configuração tem que estar implementando a interface **`WebMvcConfigurer`** pois utilizaremos um método de sua assinatura chamado **`addCorsMappings()`**, para configurarmos o CORS corretamente. Exemplo:

```java

@Configuration
public class WebConfig implements WebMvcConfigurer{
	@Value("${cors.originPatterns:default}")
    private String corsOriginPatterns = "";
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        var allowedOrigins = corsOriginPatterns.split(",");
        registry.addMapping("/**")
                .allowedMethods("*")
                .allowedOrigins(allowedOrigins)
                .allowCredentials(true);
    }
}
```

Explicando a implementação feita no método addCorsMapping:

- **`CorsRegistry`**, é um objeto usado para configurar políticas de CORS (Cross-Origin Resource Sharing).
- **`var allowedOrigins = corsOriginPatterns.split(",");`**
    - Aqui, você divide a string **`corsOriginPatterns`** em uma matriz de strings usando a vírgula como separador.
    - Isso significa que, se **`corsOriginPatterns`** contiver algo como **`"http://example.com,http://another-domain.com"`**, após o **`split`**, a matriz **`allowedOrigins`** conterá os valores **`"http://example.com"`** e **`"http://another-domain.com"`**.
    - Importante seguir esse padrão ou qualquer um que você implementar na definição das origens no application.properties.
- **`registry.addMapping("/**")`**
    - Aqui você está configurando a política de CORS para se aplicar a todos os caminhos da sua aplicação.
    - **`"/**"`** é um padrão que significa todos os caminhos.
- **`.allowedMethods("GET", "POST", "PUT", "DELETE")`**
    - Define quais métodos HTTP são permitidos nas solicitações CORS.
    - Neste caso, estão sendo permitidos os métodos GET, POST, PUT e DELETE.
    - Podemos usar **`.allowedMethods("*")`** para permitir solicitações em qualquer método HTTP.
- **`.allowedOrigins(allowedOrigins)`**
    - Especifica quais origens estão autorizadas a acessar os recursos da sua aplicação.
    - As origens são provenientes dos valores obtidos após o **`split`** da variável **`corsOriginPatterns`**.
- **`.allowCredentials(true)`**
    - Isso permite que as credenciais (como cookies e cabeçalhos de autenticação) sejam incluídas nas solicitações CORS.