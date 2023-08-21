# Implementando o CORS no Controller

Em aplicações Spring podemos habilitar o CORS de diferentes maneiras, aqui uma maneira:


### Habilitando nos Controllers:

Podemos adicionar a annotation **`@CrossOrigin`** na classe controller, se não informamos nada na annotation nós permitimos que qualquer origem acesse os endpoints daquele controller.

Podemos adicionar o **`@CrossOrigin`** em cada operação específica (métodos no controller) ao invés de se adicionar na classe.

Temos alguns parâmetros possíveis que podemos passar na annotation **`@CrossOrigin`**:

- origins, informa as origens permitidas para aquela operação

Exemplos:

```java
@RestController
@RequestMapping("/api/v1/person")
@CrossOrigin
public class PersonController {
}
```

Ou nos operadores:

```java
@CrossOrigin(origins = {"http://localhost:8080", "https://erudio.com.br"})
@PostMapping(
	consumes = {MediaType.JSON, MediaType.XML, MediaType.YML},
  produces = {MediaType.JSON, MediaType.XML, MediaType.YML})

public PersonDTO save(@RequestBody PersonDTO person){
	return personService.save(person);
}
```