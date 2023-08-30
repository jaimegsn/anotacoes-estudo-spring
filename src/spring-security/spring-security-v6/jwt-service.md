# Criando o JwtService

### Recapitulando a informação abordada na visão geral (arquitetura) do Spring Security v6:

**`JwtService`** , após uma verificação básica inicial do **`JWTAuthenticationFilter`** apenas para saber se o token é um token JWT, precisamos agora validar se o token JWT é realmente um token válido e para isso criaremos uma classe **`JwtService`** que será responsável por lidar com a criação, validação e gerenciamento de tokens JWT, essa classe encapsula a lógica necessária para trabalhar com JWTs, permitindo que outros componentes da aplicação interajam com eles de maneira mais simples e organizada. As responsabiliddades do **`JwtService`**, podem incluir:

- Criação de Tokens JWT
- Validação de Tokens
- Extração de dados do token
- Renovação do Token
- Revogação do Token

**Essa é uma implementação utilizando determinadas bibliotecas**, porém existem outras bibliotecas capazes de fazer o mesmo, então vai depender da escolha da biblioteca mas resumidamente o que o JwtService precisa ter é:

- Método para conseguir gerar um token JWT

- Método para verificar se é um token válido (Comparando o username extraido do token com o username de UserDetails, que posteriormente na classe JwtAuthenticationFilter será puxado do banco, se os nomes forem iguais e o token não estiver expirado, o token é valido)

- Método para verificar se o token não está expirado.

- Método para extrair o username do token

- Método para extrair a data da expiração do token

- Método para extrair qualquer claim desejada

- Método ou variável que tenha a informação da chave responsável para assinar e verificar tokens

### Dependências necessárias para a implementação:

Essa implementação está utilizando as bibliotecas abaixo:

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
import java.util.HashMap;
import java.util.Map;
import java.util.function.Function;

@Service
public class JwtService {

    private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";

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

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver){
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    public String extractUsername(String token){
        return extractClaim(token, Claims::getSubject);
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

    public String generateToken(UserDetails userDetails){
        return generateToken(new HashMap<>(), userDetails);
    }

    public boolean isTokenValid(String token, UserDetails userDetails){
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername())) && !isTokenExpired(token);
    }

    private boolean isTokenExpired(String token){
        return extractExpiration(token).before(new Date());
    }

    private Date extractExpiration(String token){
        return extractClaim(token, Claims::getExpiration);
    }
}
```

- **`SECRET_KEY`** é uma chave secreta usada para assinar e verificar os tokens JWT, essa chave é usada para garantir a integridade e autenticidade dos tokens
  ```java
  private static final String SECRET_KEY = "kSxGNqxoZ3fa2wp3ICVczlzGPlOtGSOp";
  ```
  <br>
- O método **`getSignInKey`** decodifica a chave secreta fornecida em formato Base64 e cria uma chave HMAC (usando o algoritmo SHA) que será usada para assinar e verificar os tokens.
  ```java
  private Key getSignInKey(){
    byte[] keyBytes = Decoders.BASE64.decode(SECRET_KEY);
    return Keys.hmacShaKeyFor(keyBytes);
  }
  ```
  <br>
- O método **`extractAllClaims`** é usado para extrair todas as reivindicações (claims) de um token JWT fornecido. Ele usa o método Jwts.parserBuilder() para configurar o parser do token, informando a chave de assinatura e, em seguida, extrai o corpo das reivindicações usando parseClaimsJws(token).getBody().

  ```java
  private Claims extractAllClaims(String token){
    return Jwts.parserBuilder()
        .setSigningKey(getSignInKey()) // é o segredo que foi usado para gerar o JWT
        .build()
        .parseClaimsJws(token)
        .getBody();
  }

  ```

  <br>

- O método genérico **`extractClaim`** recebe um token e uma função claimsResolver. Ele extrai todas as reivindicações (claims) do token usando o método extractAllClaims e, em seguida, aplica a função claimsResolver às reivindicações para obter um valor específico (por exemplo, o nome de usuário).

  ```java
    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver){
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }
  ```

  A interface **`Function`** é parte do Java e representa um contrato para uma função que aceita um argumento de um tipo e retorna um resultado de outro tipo. No código a interface **`Function<Claims, T>`** é usada para representar uma função que aceita um objeto do tipo **`Claims`** (que é uma parte do JWT que contém as reivindicações) e retorna um resultado de tipo genérico T. Isso é útil para extrair informações específicas das reivindicações(claims) de um token.
  <br>

- O método **`extractUsername`** recebe um token como entrada e usa o método genérico extractClaim para extrair o nome de usuário (subject) contido no token.

  ```java
    public String extractUsername(String token){
        return extractClaim(token, Claims::getSubject);
    }
  ```

  **`extractClaim(token, Claims::getSubject)`**, o tipo **`T`** é inferido como String, pois getSubject retorna uma string. Ou quando você chama **`extractClaim(token, claims -> claims.get("expiryDate", Date.class))`**, o tipo T é inferido como Date.
  <br>

- O método **`generateToken`** cria um novo token JWT. Ele recebe um mapa de reivindicações extras (que podem ser informações adicionais a serem incluídas no token) e os detalhes do usuário autenticado. O método **`Jwts.builder()`** é usado para construir o token, onde as reivindicações são definidas, incluindo o assunto (nome de usuário), data de emissão e expiração, bem como a chave de assinatura.

  ```java
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
  ```

- **`isTokenValid`**: Este método verifica se um token JWT é válido para um determinado usuário, com base nas informações contidas no token e nas informações do usuário fornecidas.

  - Ele começa chamando **`extractUsername(token)`** para extrair o nome de usuário (subject) contido no token.
  - Em seguida, ele compara o nome de usuário extraído do token com o nome de usuário contido em userDetails. Isso verifica se o token pertence ao usuário fornecido.
  - Além disso, ele chama **`isTokenExpired(token)`** para verificar se o token expirou.
  - A expressão completa **`return (username.equals(userDetails.getUsername())) && !isTokenExpired(token);`** retorna true se o nome de usuário no token corresponder ao nome de usuário do UserDetails e se o token não tiver expirado.

  ```java
  public boolean isTokenValid(String token, UserDetails userDetails){
    final String username = extractUsername(token);
    return (username.equals(userDetails.getUsername())) && !isTokenExpired(token);
  }
  ```

- **`isTokenExpired`**: Este método verifica se um token JWT expirou.

  - Ele começa chamando **`extractExpiration(token)`** para extrair a data de expiração do token.
  - Em seguida, ele compara a data de expiração extraída com a data atual (obtida usando **`new Date()`**).
  - Se a data de expiração for anterior à data atual, isso significa que o token expirou, e o método retorna true.

  ```java
  private boolean isTokenExpired(String token){
    return extractExpiration(token).before(new Date());
  }
  ```

- **`extractExpiration`**: Este método extrai a data de expiração (exp claim) de um token JWT.

  - Ele chama o método genérico **`extractClaim(token, Claims::getExpiration)`** para extrair a data de expiração do token.
  - O método **`extractClaim`** extrai as reivindicações do token e aplica a função **`Claims::getExpiration`** para obter a data de expiração.
  - O resultado é a data de expiração do token, que é então retornado pelo método.

  ```java
  private Date extractExpiration(String token){
    return extractClaim(token, Claims::getExpiration);
  }
  ```
