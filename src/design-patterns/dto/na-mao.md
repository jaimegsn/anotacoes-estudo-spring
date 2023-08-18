# Na Mão

- Criamos um pacote chamada `dto` seguido de um pacote com a versão da API por exemplo: `“dto.v1”` o pacote v1, isso vai ser importante para o versionamento da API.
- Dentro do pacote da versão da API criaremos as classes DTO’s, aqui um exemplo:

  ```java
  public class PersonDTOV1 implements Serializable {
      public PersonDTOV1() {
      }
      private String firstName;
      private String lastName;
      private String address;
      private String gender;
  	//Getters e Setters, Hash e Equals
  }
  ```

  Depois colocaremos um conversor de DTO para o objeto normal e vice versa no service para realizar as operações, exemplo:

  ```java
  public PersonDTOV1 save(PersonDTOV1 personDTO){
  	Person person = convertPersonDtoToPerson(personDTO);
  	return convertPersonToPersonDto(personRepository.save(person));
  }

  private Person convertPersonDtoToPerson(PersonDTOV1 personDTO){
  	Person person = new Person();
  	person.setFirstName(personDTO.getFirstName());
  	person.setLastName(personDTO.getLastName());
  	person.setAddress(personDTO.getAddress());
  	person.setGender(personDTO.getGender());
  	return person;
  }
  private PersonDTOV1 convertPersonToPersonDto(Person person){
  	PersonDTOV1 personDTO = new PersonDTO();
  	personDTO.setFirstName(person.getFirstName());
  	personDTO.setLastName(person.getLastName());
  	personDTO.setAddress(person.getAddress());
  	personDTO.setGender(person.getGender());
  	return personDTO;
  }
  ```

  Nos controllers receberemos e retornaremos um objeto DTO, por exemplo `PersonDTO`.
