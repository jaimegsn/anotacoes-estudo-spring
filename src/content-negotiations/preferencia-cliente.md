# Preferência do cliente no formato do conteúdo

Podemos receber do cliente a preferência de como ele quer o conteúdo por query params (“localhost:8080/api/v1/person&mediaType=XML”) ou por parâmetros no HEADER na requisição HTTP, a opção por Header deixa a URL mais limpa.

Definimos isso em uma classe de configuração, onde nela vamos definir o tipo de parâmetro que vamos utilizar.

Criamos uma classe de configuração e implemetamos nela a interface **`WebMvcConfigure`**, os métodos dessa interface irão nos permitir configurar vários formatos para a nossa API como JSON, XML… e também qual parâmetro queremos utilizar, se é por Query Params ou Header da requisição HTTP.
Iremos sobrescrever o método **`configureContentNegotiations(configure)`** :

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    // Com Query Params:
    @Override
    public void configureContentNegotiation
    (ContentNegotiationConfigurer configurer) {

        configurer.favorParameter(true)
                .parameterName("mediaType")
                .ignoreAcceptHeader(true)
                .useRegisteredExtensionsOnly(false)
                .defaultContentType(MediaType.APPLICATION_JSON)
                .mediaType("json", MediaType.APPLICATION_JSON)
                .mediaType("xml", MediaType.APPLICATION_XML);
    }

    // Com Header:
    @Override
    public void configureContentNegotiation
    (ContentNegotiationConfigurer configurer) {

        configurer.favorParameter(false)
                .ignoreAcceptHeader(false)
                .useRegisteredExtensionsOnly(false)
                .defaultContentType(MediaType.APPLICATION_JSON)
                .mediaType("json", MediaType.APPLICATION_JSON)
                .mediaType("xml", MediaType.APPLICATION_XML);
    }
}
```

Dentro do método configureContentNegotiations, iremos chamar alguns métodos para concluir a configuração:

- **`favorParameter(true);`** libera o uso do query param

- **`parameterName("mediaType")`**; informa o nome do parâmetro, caso estejamos utilizando query params, caso não, não colocar esse método.

- **`ignoreAcceptHeader(true)`**; quando true ignora o uso de parâmetros no header da requisição http.

- **`useRegisteredExtensionsOnly(false)`**; quando false não permite o uso de extensões para determinar o formato desejado.

- **`defaultContentType(MediaType.APPLICATION_JSON);`** define o tipo de formato padrão, no caso JSON.

- **`mediaType("json", MediaType.APPLICATION_JSON);`** Define todos os tipos de formatos aceitos, podemos repetir esse método várias vezes.

---

### Colocar parâmetros no Header usando o postman

Na aba Headers, colocar em KEY = ACCEPT, e em Value colocar o tipo de conteúdo, por exemplo: application/xml, application/json