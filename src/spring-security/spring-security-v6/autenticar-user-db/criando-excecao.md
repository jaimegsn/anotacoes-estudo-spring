# Criando uma exceção personalizada

Exceções de falha de autenticação devem herdar a seguinte classe: **`import org.springframework.security.core.AuthenticationException`**

Exemplo:

```java
@ResponseStatus(HttpStatus.FORBIDDEN)
public class InvalidJwtAuthenticationException extends AuthenticationException{
    public InvalidJwtAuthenticationException(String ex){
        super(ex);
    }
}
```