# Path Params, (”/users/1”)

Passamos o parâmetro diretamente na URL.
Exemplo no código:

```java
@GetMapping(value = "/{id}")
public ResponseEntity<User> findById(@PathVariable Long id) {
	//....
}
```

Ou:

```java
@GetMapping(value = "/{id}")
public ResponseEntity<User> findById(@PathVariable(value = "id") Long id) {
	//....
}
```

A URL de acesso ao endpoint ficará : `‘/users/1’`, sendo ‘1’ qualquer número e ele representa o id do usuário.
<br>

O id do usuário é referenciado dentro dos parâmetros do método `findById()` com uma annotation `@PathVariable` depois é especificado o tipo do parâmetro e o seu nome, agora é só utiliza-lo dentro do método.

- O uso de **`@PathVariable`** exige que os parâmetros sejam incluídos diretamente na URL, o que pode levar a duplicações de URLs gerando conflitos.
