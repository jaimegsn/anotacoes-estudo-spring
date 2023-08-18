# @RequestMapping

O **`@RequestMapping`** é uma anotação que mapeia todas as requisições recebidas pelo controlador.

Porém, podemos especificar qual tipo de requisição (GET, POST, etc.) queremos tratar.

Embora seja amplamente usado em sistemas legados, em projetos modernos, é comum usá-lo na classe para personalizar a URL de forma mais específica.

Exemplo:

```java
@RequestMapping(value="/users")
public class ClasseControladora{

	@RequestMapping(value="/{id}", method = RequestMethod.GET)
	public Person findById(@PathVariable Long id){
		//...
	}

    @RequestMapping(method = RequestMethod.GET)
	public Person findAll(){
		//...
	}
}
```

Com `@RequestMapping(value = "/users")` personalizamos a URL indicando que só conseguimos acessar os métodos do controller pela url: `“/users”`.

O `findById` é acessado quando passamos um parâmetro na URL, exemplo: `“/users/1”`.

O `findAll` como não tem um value, é acessado apenas por `“/users”`

O method de `@RequestMapping( method = RequestMethod.GET)` indica com qual verbo HTTP estamos lidando naquele método.
