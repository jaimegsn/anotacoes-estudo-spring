# Customizando o Swagger

Na classes controller do nosso projeto adicionaremos a customização.

Na classe em si podemos adicionar a annotation **`@Tag`**, onde podemos com ela especificar o nome do que se trata a operação do endpoint e a sua descrição, exemplo:

```java
@RestController
@RequestMapping("/api/v1/person")
@Tag(name = "People", description = "Endpoints for Managing People")
public class PersonController {
	//...
}
```

---

Nos métodos podemos adicionar a annotation **`@Operation`**, onde nela podemos adicionar os seguintes parâmetros:

- **`summary`**: É um breve resumo do que a operação faz. Permite no minimo 120 caracteres
- **`description`**: É uma descrição mais detalhada da operação.
- **`tags`**: São palavras-chave que ajudam a categorizar a operação. Por exemplo, uma operação é relacionada às pessoas, é uma boa prática combina-lo com o name do **`@Tag`** na classe.
- **`responses`**: Define as respostas possíveis para a operação.

Exemplo em código:

```java
@GetMapping(produces = {MediaType.JSON, MediaType.XML, MediaType.YML})
@Operation(summary = "Finds all People",
    description = "Finds all People",
    tags = {"People"},
    responses = {
        @ApiResponse(description = "Success", responseCode = "200", content = {
	        @Content(mediaType = MediaType.JSON,
               array = @ArraySchema(schema = @Schema(implementation = PersonDTO.class)))
        }),
        @ApiResponse (description = "Bad Request", responseCode = "400", content = @Content),
        @ApiResponse (description = "Unauthorized", responseCode = "401", content = @Content),
        @ApiResponse (description = "Not Found", responseCode = "404", content = @Content),
        @ApiResponse (description = "Internal Error", responseCode = "500", content = @Content)
    })
    public List<PersonDTO> findAll(){
        return personService.findAll();
    }
```

Dento do parâmetro **`responses`** teremos as possíveis repostas daquela operação, tanto para operações realizadas com sucesso quanto para falhas.  Para cada resposta colocamos a annotation **`@ApiResponse`**, onde nela podemos adicionar os seguintes parâmetros:

- **`description`**: É uma descrição textual sobre a código HTTP da resposta da operação, por exemplo "Bad Request".
- **`responseCode`**: Representa o código de status HTTP da resposta.
- **`content`**: Um exemplo do conteúdo que virá na resposta, indicamos o conteúdo com a annotation **`@Content`**, onde nele podemos adicionar os seguintes parâmetros:

  - **`mediaType=`**, que irá indicar o tipo de dado que a resposta irá produzir, como JSON, XML…
  - E podemos também adicionar o schema(estrutura) do objeto da resposta

    - **`schema`**, propriedade que define o schema(estrutura) do objeto que virá na resposta daquela operação, usado quando a resposta trás um único objeto, é usado em conjunto com a annotation **`@Schema`**.
    - **`array`**, propriedade que define o schema(estrutura) quando se trata de coleções, usado em conjunto com as annotations **`@ArraySchema`** e **`@Schema`**
    - Exemplo em código:

    ```java
    @ApiResponse(
    	description = "Success",
    	responseCode = "200",
    	content = {
    		@Content(
    			mediaType = MediaType.JSON,
    			schema = @Schema(implementation = PersonDTO.class))
    }),

    @ApiResponse(
    	description = "Success",
    	responseCode = "200",
    	content = {
    		@Content(
    			mediaType = MediaType.JSON,
    			array = @ArraySchema(schema = @Schema(implementation = PersonDTO.class)))
    }),

    @ApiResponse(
    	description = "Bad Request",
    	responseCode = "400",
    	content = @Content)
    ```

    Em operações que resultaram em falhas podemos deixar o **`@Content`** sem nenhum parâmetro que o Spring se encarrega de carregar um conteúdo padrão
