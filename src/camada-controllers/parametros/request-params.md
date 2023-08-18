# Query ou Request Params, (”?q=termo&pagina=2”)

Com Request Param passamos o parâmetro de uma maneira diferente por query string `("?q=termo&pagina=2”)`, assim: `localhost:8080/pessoas/find?name=pedro`

Exemplo no código:

```java
@GetMapping(value = "/find")
public Pessoa findByName(@RequestParam(required = false) String name){
	//..
}
```

- O uso de **`required=false`** ou **`required=true`** define se o parâmetro é obrigatório ou opcional em uma requisição.

- Ao usar **`@RequestParam`**, os parâmetros podem ser incluídos na URL como parte da query string ("?q=termo&pagina=2”), permitindo que vários parâmetros sejam enviados para uma única URL/Endpoint.

- Isso evita a necessidade de criar várias URLs/Endpoints para diferentes combinações de parâmetros.

- Em contraste, o uso de **`@PathVariable`** exige que os parâmetros sejam incluídos diretamente na URL, o que pode levar a duplicações de URLs gerando conflitos.

- O uso de **`@RequestParam`** simplifica o design da API, permitindo que os parâmetros sejam enviados como parte da query string ("?q=termo&pagina=2”) e eliminando a duplicação de URLs.
