# Acessar as informações do usuário autenticado

Talvez queiramos acessar as informações do usuário que foi autenticado em algum método do nosso controller, para isso utilizaremos a annotation **`@AuthenticationPrincipal UserDetails userDetails`** no parâmetro da operação.

Esse parâmetro como explicitado deve ser do tipo **`UserDetails`**, exemplo em código:

```java
@RestController
@RequestMapping("/api/v1/user")
@EnableMethodSecurity
public class UserController {

	@PostMapping
	@PreAuthorize("hasRole('ADMIN')")
	public ResponseEntity<String> createUser
		(@AuthenticationPrincipal UserDetails userDetails){

		return ResponseEntity.ok().body(userDetails.toString());
	}
}
```

Terá essas informações no objeto UserDetails:

org.springframework.security.core.userdetails.User

[Username=admin,

Password=[PROTECTED],

Enabled=true,

AccountNonExpired=true,

credentialsNonExpired=true,

AccountNonLocked=true,

Granted Authorities=[ROLE_ADMIN]]
