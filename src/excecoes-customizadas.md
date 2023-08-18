# Exceções Customizadas

### Criando classe de Exceção:

A maioria das exceções lançadas em uma aplicação spring são **`RuntimeException`**, isso é uma prática comum porque são exceções que não precisam ser declaradas explicitamente no método ou serem tratadas com bloco try-catch (unchecked exceptions).

Então normalmente a nossa classe de exceção irá herdar RuntimeException, também adicionaremos uma annotation **`@ResponseStatus`** com o status HTTP que desejamos lançar juntamente com a exceção.

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class BadRequestException extends RuntimeException {
    public BadRequestException(String message) {
        super(message);
    }
}
```

---

### Criando uma classe com uma resposta personalizada.

Precisamos criar uma classe que irá representar a resposta em formato JSON da exceção para o cliente, essa classe irá conter informações relevantes sobre a exceção, como a data em que ocorreu, a mensagem de erro e a descrição da solicitação, essas informações são encapsuladas no objeto dessa classe e iremos manda-lo como resposta á exceção lançada.

**Lembrar de implementar Serializable**

Exemplo da classe:

```java
import java.util.Date;

public class ExceptionResponse implements Serializable {
    private static final long serialVersionUID = 1L;
    private Date timestamp;
    private String message;
    private String details;

    public ExceptionResponse(Date timestamp, String message, String details) {
        this.timestamp = timestamp;
        this.message = message;
        this.details = details;
    }

    public Date getTimestamp() {
        return timestamp;
    }

    public String getMessage() {
        return message;
    }

    public String getDetails() {
        return details;
    }
}
```

---

### Controller Advide e Handler Global.

"Controller Advice" é uma anotação utilizada em classes que atuam como interceptadores de exceções em todo o aplicativo.

Imagine que você está planejando uma grande festa em sua casa. Você convida vários amigos, mas há sempre a possibilidade de ocorrerem contratempos. Para lidar com isso, você pode designar um amigo experiente como "conselheiro" (controller advice) para lidar com qualquer problema que possa surgir durante a festa.

Então usando a lógica da analogia criaremos um classe Handler para ouvir todas as exceções lançadas na aplicação, Exemplo:

```java
import br.com.erudio.exceptions.ExceptionResponse;
import br.com.erudio.exceptions.UnsupportedMathOperationException;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.context.request.WebRequest;

import java.util.Date;

@ControllerAdvice
@RestController
public class RestExceptionHandler{

    //Exceção especifica
    @ExceptionHandler(UnsupportedMathOperationException.class)
    public final ResponseEntity<ExceptionResponse> handleUnsupportedMathOperationExceptions(
            UnsupportedMathOperationException e, WebRequest request) {
        ExceptionResponse er = new ExceptionResponse(
                new Date(),
                e.getMessage(),
                request.getDescription(false));

        return ResponseEntity.badRequest().body(er);
    }

    //Exceção mais genérica
    @ExceptionHandler(Exception.class)
    public final ResponseEntity<ExceptionResponse> handleGenericExceptions(
        Exception e, WebRequest request) {
        ExceptionResponse er = new ExceptionResponse(
                new Date(),
                e.getMessage(),
                request.getDescription(false));

        return ResponseEntity.internalServerError().body(er);
    }
}
```

- Adicionamos na classe as annotations `@ControllerAdvice` para ouvir todas as exceções da aplicação, `@RestController` porque é uma aplicação rest e precisamos retornar o erro como uma API Rest para o cliente.

- Adicionamos no método a annotation `@ExceptionHandler(Exceção)` para executar aquele método específico para aquela exceção

- Lembrar de sempre tratar a exceção mais genérica (`Exception.class`) ao criar o handler

- A classe **`WebRequest`** no Spring Framework é uma abstração que representa uma solicitação web recebida pelo servidor. Ela fornece métodos para acessar informações sobre a solicitação, como cabeçalhos, parâmetros, cookies, método HTTP, entre outros.

  O objetivo do parâmetro **`WebRequest`** nesse contexto é fornecer informações adicionais sobre a solicitação web (’uri = /sum/2/3’) que causou a exceção.

- O método **`request.getDescription()`** retorna uma descrição detalhada da requisição, incluindo informações como o método HTTP, o URI da requisição, os parâmetros e os cabeçalhos. Ao passar o valor **`false`**, essas informações detalhadas não serão incluídas na descrição e apenas informações básicas sobre a requisição serão retornadas.

- E o `ExceptionResponse` criado no passo anterior irá no `ResponseEntity`.
