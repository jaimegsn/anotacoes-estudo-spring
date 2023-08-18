# Produces e Consumes

Podemos definir o tipo de conteúdo que um determinado método da classe controladora irá consumir e produzir, como JSON,XML… para isso utilizaremos constantes da classe MediaType

Não são obrigatórias, mas são utilizadas para fornecer informações adicionais sobre o tipo de conteúdo (media type) que um método de um controlador pode produzir ou consumir. Elas foram introduzidas no contexto do desenvolvimento de APIs RESTful para especificar os tipos de dados que um endpoint pode manipular.

```java
@RestController
@RequestMapping(value = "/users")
public class UserController {

	@GetMapping(value = "/{id}", produces = MediaType.APPLICATION_JSON_VALUE)
	public ResponseEntity<User> findById(@PathVariable Long id) {
		//....
	}
	@PostMapping(consumes = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<User> insert(@RequestBody User user) {
        //....
	}

	@RequestMapping(method = RequestMethod.POST,
		            consumes = MediaType.APPLICATION_JSON_VALUE,
		            produces = MediaType.APPLICATION_JSON_VALUE)
	public Person create(@RequestBody Person person) throws Exception{
		return personServices.createPerson(person);
	}

}
```
