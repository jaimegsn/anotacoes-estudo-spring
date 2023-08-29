# Criando o JwtService

### Recapitulando a informação abordada na visão geral (arquitetura) do Spring Security v6:

**`JwtService`** , após uma verificação básica inicial do **`JWTAuthenticationFilter`** apenas para saber se o token é um token JWT, precisamos agora validar se o token JWT é realmente um token válido e para isso criaremos um **`JwtService`** que será responsável por lidar com a criação, validação e gerenciamento de tokens JWT, essa classe encapsula a lógica necessária para trabalhar com JWTs, permitindo que outros componentes da aplicação interajam com eles de maneira mais simples e organizada. As responsabiliddades do **`JwtService`**, podem incluir:

- Criação de Tokens JWT
- Validação de Tokens
- Extração de dados do token
- Renovação do Token
- Revogação do Token

asdas

### Dependências:

```xml
<!-- https://mvnrepository.com/artifact/io.jsonwebtoken/jjwt-api -->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
</dependency>
```

### Código e explicação:

```java
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.io.Decoders;
import io.jsonwebtoken.security.Keys;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Service;

import java.security.Key;
import java.util.Date;
import java.util.Map;
import java.util.function.Function;

@Service
public class JwtService {

    private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";

    public String extractUsername(String token){
        return extractClaim(token, Claims::getSubject);
    }

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver){
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    public String generateToken(
            Map<String, Object> extraClaims,
            UserDetails userDetails){

        return Jwts
                .builder()
                .setClaims(extraClaims)
                .setSubject(userDetails.getUsername())
                .setIssuedAt(new Date(System.currentTimeMillis()))
                .setExpiration(new Date(System.currentTimeMillis()+ 1000 * 60 * 24))
                .signWith(getSignInKey(), SignatureAlgorithm.HS256)
                .compact();
    }

    private Key getSignInKey(){
        byte[] keyBytes = Decoders.BASE64.decode(SECRET_KEY);
        return Keys.hmacShaKeyFor(keyBytes);
    }

    private Claims extractAllClaims(String token){
        return Jwts.parserBuilder()
                .setSigningKey(getSignInKey()) // é o segreddo que foi usado para gerar o JWT
                .build()
                .parseClaimsJws(token)
                .getBody();
    }
}
```

- **`SECRET_KEY`** é uma chave secreta usada para assinar e verificar os tokens JWT, essa chave é usada para garantir a integridade e autenticidade dos tokens
  ```java
  private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";
  ```
- O método genérico extractClaim recebe um token e uma função claimsResolver. Ele extrai todas as reivindicações (claims) do token usando o método extractAllClaims e, em seguida, aplica a função claimsResolver às reivindicações para obter um valor específico (por exemplo, o nome de usuário).

  ```java
    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver){
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }
  ```

  A interface Function é parte do Java e representa um contrato para uma função que aceita um argumento de um tipo e retorna um resultado de outro tipo. No código a interface **`Function<Claims, T>`** é usada para representar uma função que aceita um objeto do tipo **`Claims`** (que é uma parte do JWT que contém as reivindicações) e retorna um resultado de tipo genérico T. Isso é útil para extrair informações específicas das reivindicações(claims) de um token.

- O método extractUsername recebe um token como entrada e usa o método genérico extractClaim para extrair o nome de usuário (subject) contido no token.

  ```java
    public String extractUsername(String token){
        return extractClaim(token, Claims::getSubject);
    }
  ```

  **`extractClaim(token, Claims::getSubject)`**, o tipo **`T`** é inferido como String, pois getSubject retorna uma string. Ou quando você chama **`extractClaim(token, claims -> claims.get("expiryDate", Date.class))`**, o tipo T é inferido como Date,

- O método extractUsername recebe um token como entrada e usa o método genérico extractClaim para extrair o nome de usuário (subject) contido no token.
  ```java
  private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";
  ```
- O método extractUsername recebe um token como entrada e usa o método genérico extractClaim para extrair o nome de usuário (subject) contido no token.
  ```java
  private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";
  ```
- O método extractUsername recebe um token como entrada e usa o método genérico extractClaim para extrair o nome de usuário (subject) contido no token.
  ```java
  private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";
  ```
- O método extractUsername recebe um token como entrada e usa o método genérico extractClaim para extrair o nome de usuário (subject) contido no token.
  ```java
  private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";
  ```
