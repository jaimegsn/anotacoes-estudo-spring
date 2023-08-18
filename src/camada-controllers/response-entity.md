# Response Entity

O tipo **`ResponseEntity<T>`** no Java é usado para retornar uma resposta HTTP personalizada. Ele permite controlar o corpo da resposta, os cabeçalhos HTTP e o status de resposta.

O **`ResponseEntity<T>`** é um tipo genérico que converte qualquer tipo de dado para o formato JSON.

Existem duas formas de criar um objeto **`ResponseEntity`**: a primeira é usando o operador **`new`** para instanciar um objeto e passar o corpo, o cabeçalho e o status como argumentos do construtor. O status é o único parâmetro obrigatório:

```java
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;

@RestController
@RequestMapping(value = "/users")
public class UserResource {

    @GetMapping
    public ResponseEntity<User> findAll() {
		// Criando Header
        HttpHeaders httpHeaders = new HttpHeaders(); // Uma coleção de Headers
        httpHeaders.add("header-name","header-value");

        User user = new User(1L, "Jaime", "jaime@example.com", "8888888");

		//Criando obj ResponseEntity, Construtor -> body, header, status
        return new ResponseEntity<>(user, httpHeaders, HttpStatus.CREATED);
    }
}
```

A segunda forma é usando métodos estáticos da classe **`ResponseEntity<T>`**:

```java
import org.springframework.http.HttpStatus;

@RestController
@RequestMapping(value = "/users")
public class UserResource {

    @GetMapping
    public ResponseEntity<User> findAll() {
        User user = new User(1L, "Jaime", "jaime@example.com", "8888888");
        return ResponseEntity
                .status(HttpStatus.CREATED)
                .header("header-name","header-value")
                .body(user);
    }
}
```

A vantagem de usar ResponseEntity<T> é que você tem controle total sobre a resposta HTTP e pode personalizá-la de acordo com suas necessidades.

Por exemplos, podemos retornar `no content` nos casos do verbo HTTP delete:

```java
@DeleteMapping(value = "/{id}")
public ResponseEntity<?> delete(@PathVariable(value="id") Long id){
    personService.delete(id);
    return ResponseEntity.noContent().build();
}
```
