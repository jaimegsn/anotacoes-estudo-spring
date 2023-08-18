# Request Body

Também podemos receber dados no corpo das requisições HTTP, principalmente quando se trabalha com objetos complexos, em vez de receber cada atributo separadamente com parâmetros na url.

Utilizamos a annotation **`@RequestBody`** para mapear o corpo da requisição HTTP diretamente para um objeto, essa annotation indica que o conteúdo da requisição HTTP deve ser convertido em um objeto Java.
Exemplo:

```java
@PostMapping("/users")
public ResponseEntity<String> createUser(@RequestBody User user) {
    // Lógica para criar um novo usuário com o objeto recebido
    // ...
    return ResponseEntity.ok("Usuário criado com sucesso");
}
```

Dessa forma, o Spring irá realizar a conversão automática do JSON recebido no corpo da requisição para um objeto **`User`**. Assim, é possível acessar os atributos do objeto no método do controller ou envia-lo para a camada de serviços e realizar as operações necessárias.