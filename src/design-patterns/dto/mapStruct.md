# Map Struct

Link: [mapstruct.org](https://mapstruct.org/)

1. Criamos uma camada chamada dto seguido de um pacote coma versão da API por exemplo: `“dto.v1”` o pacote v1 vai ser importante para o versionamento da API.
2. Dentro do pacote da versão da API criaremos as classes DTO’s, aqui um exemplo:

   ```java
   public class PersonDTO implements Serializable {
       public PersonDTO() {
       }
       private String firstName;
       private String lastName;
       private String address;
       private String gender;
   	//Getters e Setters, Hash e Equals
   }
   ```

3. Agora adicionamos a dependência no POM.XML, verificar no site se existe uma versão mais atualizada.

   ```xml
   <properties>
   	<org.mapstruct.version>1.5.5.Final</org.mapstruct.version>
   </properties>

   <dependency>
   	<groupId>org.mapstruct</groupId>
   	<artifactId>mapstruct</artifactId>
   	<version>${org.mapstruct.version}</version>
   </dependency>

   <build>
       <plugins>
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-compiler-plugin</artifactId>
               <version>3.8.1</version>
               <configuration>
                   <source>1.8</source> <!-- Versão JDK do seu projeto -->
                   <target>1.8</target> <!-- Versão JDK do seu projeto -->
                   <annotationProcessorPaths>
                       <path>
                           <groupId>org.mapstruct</groupId>
                           <artifactId>mapstruct-processor</artifactId>
                           <version>${org.mapstruct.version}</version>
                       </path>
                       <!-- other annotation processors -->
                   </annotationProcessorPaths>
               </configuration>
           </plugin>
       </plugins>
   </build>
   ```

4. Criamos um pacote chamado `‘mapper’` e criamos classes abstratas ou interfaces para criar os métodos de conversão abstratos, por exemplo criamos uma interface ou classe abstrata: PersonMapper:

   ```java
   import org.mapstruct.Mapper;
   import org.mapstruct.factory.Mappers;

   @Mapper(componentModel = "spring")
   public abstract class PersonMapper {
       // Precisamos criar uma forma de pegar a instância do Mapper
       private static final PersonMapper INSTANCE = Mappers.getMapper(PersonMapper.class);
       public abstract Person toPerson(PersonDTO personDTO);
       public abstract PersonDTO toPersonDTO (Person person);
   	   public abstract List<PersonDTO> toListPersonDTO (List<Person> listPerson);

   }
   ```

   - Colocamos a annotation: `@Mapper(componentModel = "spring")` , o componentModel serve para ele tratar o Mapper como um componente Spring caso queiramos injetar ele como alguma dependência.

   - Criamos uma variável que servirá como uma instância do Mapper: `public static final PersonMapper *INSTANCE*`
   
   - Depois criamos métodos de conversão da entidade para entidadeDTO e vice-versa

5. Depois é só fazermos as conversões, exemplo:

   ```java
   public PersonDTO save(PersonDTO personDTO){
   	Person person = PersonMapper.INSTANCE.toPerson(personDTO);
   	return PersonMapper.INSTANCE.toPersonDTO(personRepository.save(person));
   }

   public List<PersonDTO> findAll(){
   	try{
   		List<Person> personList = personRepository.findAll();
   		return PersonMapper.INSTANCE.toListPersonDTO(personList);
   	}catch (RuntimeException e){
   		throw new ResourceNotFoundException("Resource not found");
   	}
   }
   ```

6.
