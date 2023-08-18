# HATEOAS em uma Listagem

Em uma listagem de objetos temos que iterar e para cada objeto e adicionar o link dinâmico, exemplo:

```java
List<PersonDTO> personDTOList = ...

personDTOList.forEach(p -> p.add(linkTo(methodOn(
				PersonController.class).findById(p.getIdPerson())).withSelfRel()));
```
