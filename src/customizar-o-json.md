# Customizar o JSON (Custom JSON Serialization)

As vezes podemos querer customizar o JSON que enviamos para o nosso cliente, podemos querer mudar o nome de um campo, tirar alguns atributos e etc.

```java
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonPropertyOrder;
import com.fasterxml.jackson.annotation.JsonProperty;

@JsonPropertyOrder({"address","first_name","last_name","gender"})
public class PersonDTO implements Serializable {
    public PersonDTO() {
    }

    @JsonProperty("first_name")
    private String firstName;

    @JsonProperty("last_name")
    private String lastName;

    private String address;

    @JsonIgnore
    private String gender;
}
```

- Utilizaremos a annotation `@JsonIgnore` nos campos que queremos omitir.
- Utilizaremos a annotation `@JsonProperty("new_name")` no atributo com o novo nome do campo, para mudar o nome do campo que aparecerá no JSON
- Utilizaremos a annotation `@JsonPropertyOrder({"field2","field1"})` na classe com a ordem dos atributos que queremos que apareça no JSON
