# Formato YML precisa de um passo a mais

Precisamos criar uma classe que irá converter o YAML para uma mensagem HTTP, exemplo:

```java
package br.com.erudio.serialization.converter;
import com.fasterxml.jackson.annotation.JsonInclude;
import com.fasterxml.jackson.dataformat.yaml.YAMLMapper;
import org.springframework.http.MediaType;
import org.springframework.http.converter.json.AbstractJackson2HttpMessageConverter;

public class YamlJackson2HttpMessageConverter extends AbstractJackson2HttpMessageConverter {
    public YamlJackson2HttpMessageConverter() {
        super(new YAMLMapper().setSerializationInclusion(JsonInclude.Include.NON_NULL),
                MediaType.parseMediaType("application/x-yaml"));
        //setSerializationInclusion indica os atributos que vamos serializar
        // no caso todos os atributos que não forem nulos
    }
}
```

Agora vamos ajustar a nossa classe WebConfig:

```java
import org.springframework.http.MediaType;

@Configuration
public class WebConfig implements WebMvcConfigurer {

    // Essa constante só é necessária para o YML
    private static final MediaType MEDIA_TYPE_APPLICATION_YML = MediaType.valueOf("application/x-yaml");

    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer.favorParameter(false)
                .ignoreAcceptHeader(false)
                .useRegisteredExtensionsOnly(false)
                .defaultContentType(MediaType.APPLICATION_JSON)
                .mediaType("json", MediaType.APPLICATION_JSON)
                .mediaType("xml", MediaType.APPLICATION_XML)
                .mediaType("x-yaml", MEDIA_TYPE_APPLICATION_YML);
    }
}
```

Agora nos controllers basta adicionar o YAML/YML nos produces e consumes:

```java
@PostMapping(consumes = {MediaType.APPLICATION_JSON_VALUE, "application/x-yaml"},
     produces = {MediaType.APPLICATION_JSON_VALUE, "application/x-yaml"})
public PersonDTO save(@RequestBody PersonDTO person){
	return personService.save(person);
}
```