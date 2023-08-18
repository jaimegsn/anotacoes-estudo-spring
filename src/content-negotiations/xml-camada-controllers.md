# Adicionando XML na camada de controller

Adicionaremos no consumes e produces o novo tipo de formato XML, por exemplo:

```java
@PostMapping(
consumes = {MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE},
produces = {MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE}
)
public PersonDTO save(@RequestBody PersonDTO person){
	return personService.save(person);
}
```