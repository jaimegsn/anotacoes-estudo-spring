# Melhorando o Produces e Consumes

Dependendo da quantidade de formatos que sua API irá produzir para o cliente serão muitos parâmetros no consumes ou/e produces.

Então para isso podemos criar uma classe MediaType em um pacote utils e utiliza-lo, exemplo:

```java
package br.com.erudio.utils;

public class MediaType {
    public static final String JSON = "application/json";
    public static final String XML = "application/xml";
    public static final String YML = "application/x-yaml";
}
```

Depois basta utilizarmos eles nos produces e consumes:

```java
@GetMapping(value = "/{id}",
   produces = {MediaType.JSON, MediaType.XML})
    public PersonDTO findById(@PathVariable(value="id") Long id){
        return personService.findById(id);
    }
```