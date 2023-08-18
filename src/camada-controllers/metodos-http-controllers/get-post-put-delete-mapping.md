# @GetMapping, @PostMapping, @PutMapping, @DeleteMapping

Ao longo do tempo surgiu annotations para cada um dos métodos/verbos HTTP, para não ser necessário informamos o method no RequestMapping, apenas utilizamos a annotation certa, mas de resto segue a mesma lógica do RequestMapping, exemplo:

```java
@RestController
@RequestMapping(value = "/users")
public class UserController {

    @GetMapping(produces = {MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE})
    public ResponseEntity<User> findAll() {
        //....
    }
	@GetMapping(value = "/{id}", produces = MediaType.APPLICATION_JSON_VALUE)
	public ResponseEntity<User> findById(@PathVariable Long id) {
		//....
	}
	@PostMapping(consumes = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<User> insert(@RequestBody User user) {
        //....
    }
	@PutMapping(value = "/{id}")
    public ResponseEntity<User> update(@PathVariable Long id, @RequestBody User user) {
		//....
    }
	@DeleteMapping(value = "/{id}")
    public ResponseEntity<Void> deleteById(@PathVariable Long id) {
        //....
    }
}
```

O `@RequestMapping(value = "/users")` está apenas personalizando a URL.
Para podermos acessar os métodos do controller precisamos utilizar a url `"/users"`
