# Proteção a nível de operação no Controller

Podem existir algumas operações no nosso Controller que queremos que apenas algum tipo de usuário(role) possa executa-la, para isso utilizaremos a seguinte annotation no método do Controler: **`@PreAuthorize("hasRole('ADMIN')")`** informando a role. 

Para essa annotation funcionar também é necessário colocar a annotation **`@EnableMethodSecurity`**, em versões anteriores do Spring Security a annotation é diferente, no caso era : **`@EnableGlobalMethodSecurity(prePostEnabled = true)`** .

Exemplo em código:

```java

@RestController
@RequestMapping("/api/v1/user")
@EnableMethodSecurity
public class UserController {

	@PostMapping
	@PreAuthorize("hasRole('ADMIN')")
	public ResponseEntity<String> createUser(){
		return ResponseEntity.ok().body("User created");
	}
}
```

Dessa forma apenas usuários de tipo admin podem executar essa operação de **`createUser`**