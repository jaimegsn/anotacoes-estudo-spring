# Exemplo de um código completo implementando HATEOAS com imports estáticos

```java
import static org.springframework.hateoas.server.mvc.WebMvcLinkBuilder.linkTo;
import static org.springframework.hateoas.server.mvc.WebMvcLinkBuilder.methodOn;

public PersonDTO findById(Long id){
	Optional<Person> optPerson = personRepository.findById(id);
	PersonDTO personDTO =  PersonMapper.INSTANCE.toPersonDTO(optPerson
   .orElseThrow(() -> new ResourceNotFoundException("No records found")));

	personDTO.add(linkTo(methodOn(PersonController.class).findAll()
											 ).withRel("Listagem de pessoas"));
	return personDTO;
}
```
