# Data Binding

Algumas query strings `(”?q=termo&pagina=2”)` passadas na URL funcionam mesmo sem existir um RequestParam, isso porque o Spring possui uma funcionalidade chamada “vinculação de dados” (Data Binding).

Isso permite que seja vinculado automaticamente os valores recebidos na query string com os parâmetros do método Controller, com base no nome do parâmetro se eles forem iguais.

Exemplo:

```java
@RestController
@RequestMapping
public class ClasseControladora{

  @GetMapping
  public ResponseEntity<String> getUsuario(String nome){
      return ResponseEntity.ok().body(nome);
   }
}
```

Temos o parâmetro `"String nome"` no método `getUsuario()` da classe controladora, podemos passar um RequestParam mesmo sem ele estar definido explicitamente, assim:

- `localhost:8080/?nome=jaime`
