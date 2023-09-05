# JwtAuthenticationFilter

Após termos criado o JwtService iremos criar o filtro **`JwtAuthenticationFilter`**, onde sua função será realizar verificações no token para valida-lo, inclusive essas avaliações incluem utilizar métoddos de JwtService.

**`JwtAuthenticationFilter`** será uma classe que irá estender a classe abstrata **`OncePerRequestFilter`** do Spring, essa classe foi criada com o objetivo de facilitar a criação de filtros que devem ser executados uma única vez para cada solicitação HTTP, garantindo que essas operações não sejam repetidas, mesmo que haja múltiplos filtros na cadeia de filtros.

A classe OncePerRequestFilter possui um único método abstrato chamado **`doFilterInternal`**. Este método é onde iremos colocar a lógica do filtro que será executada uma vez por solicitação.

O método **`doFilterInternal`** recebe três argumentos:

- **HttpServletRequest**: A solicitação HTTP recebida.
- **HttpServletResponse**: A resposta HTTP que será enviada de volta ao cliente.
- **FilterChain**: O objeto que representa a cadeia de filtros restante a ser executada após o filtro atual.

### Implementação do código:

```java
import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.RequiredArgsConstructor;
import org.springframework.lang.NonNull;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;

@Component
@RequiredArgsConstructor
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtService jwtService;
    private final UserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(
            @NonNull HttpServletRequest request,
            @NonNull HttpServletResponse response,
            @NonNull FilterChain filterChain) throws ServletException, IOException {

        final String authHeader = request.getHeader("Authorization");
        final String jwtToken;
        final String userEmail;
        if(authHeader == null || !authHeader.startsWith("Bearer ")){
            filterChain.doFilter(request, response);
            return;
        }
        jwtToken = authHeader.substring(7);
        userEmail = jwtService.extractUsername(jwtToken);
        if(userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null){
            UserDetails userDetails = this.userDetailsService.loadUserByUsername(userEmail);
            if(jwtService.isTokenValid(jwtToken, userDetails)){
                UsernamePasswordAuthenticationToken authToken =
                        new UsernamePasswordAuthenticationToken(
                                userDetails,
                                null,
                                userDetails.getAuthorities());
                authToken.setDetails(
                        new WebAuthenticationDetailsSource().buildDetails(request)
                );

                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
            filterChain.doFilter(request, response);
        }
    }
}
```

- Annotations:

  **`@Component`**: Indica que essa classe é um componente gerenciado pelo Spring.
  **`@RequiredArgsConstructor`**: Do Lombok, gera um construtor com todos os campos marcados como final.
  <br>

- A variável **`jwtService`** irá ser responsável por gerenciar o JWT token que virá da requisição, como validar ele, extrair informações dele e etc, enquanto que o **`userDetailsService`** será responsável por pegar o usuário no banco de dados.

  ```java
  private final JwtService jwtService;
  private final UserDetailsService userDetailsService;
  ```

- **`authHeader`** irá receber o valor do JWT Token que estiver no header(cabeçalho) **"Authorization"**, se for nulo ou não começar com **"Bearer "** a solicitação é passada adiante para o próximo filtro sem autenticar o usuário, com o método **`filterChain.doFilter(request, response);`**.

  ```java
  final String authHeader = request.getHeader("Authorization");

  if(authHeader == null || !authHeader.startsWith("Bearer ")){
    filterChain.doFilter(request, response);
    return;
  }
  ```

- A variável **`jwtToken`** irá receber o valor do token que irá chegar no cabeçalho da requisição, enquanto que a variável **`userEmail`** irá receber o email do usuário que está no Token (**Não o do banco**), se quisermos ao invés do email poderia ser o username, porém optei por email por ser algo único de cada usuário, mas isso vai depender do sistema e do contexto dele.

  ```java
  final String jwtToken;
  final String userEmail;
    //...codes
  jwtToken = authHeader.substring(7);
  userEmail = jwtService.extractUsername(jwtToken);
  ```

  **Para pegar o token pegamos a partir do caractere 7 porque geralmente em token JWT ele começam com "Bearer " então precisamos pular esses caracteres.**

- Teremos um **`if`** que irá verificar se o email(ou username) não é nulo e se no contexto de autenticação atual já não existe uma autenticação. Isso evita reautenticação usando o mesmo token na mesma solicitação.

  ```java
  if(userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null){
    //....
  }
  ```

- Depois da verificação passamos adiante e será realizado uma consulta no banco de dados buscando o usuário de acordo com seu email(ou username) do token para verificar se o usuário realmente existe no banco de dados, essa busca retornará um objeto do tipo **`UserDetails`**, que conterá os tipos de dados necessários sobre um usuário para o Spring Security executar os processos necessários, essa busca vai ser realizada por um objeto do tipo **`UserDetailsService`**.

  ```java
  if(userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null){
    UserDetails userDetails = this.userDetailsService.loadUserByUsername(userEmail);
  }
  ```

- Agora teremos outra verificação(if), dessa vez será avaliado se o nosso token é valido de acordo com um método de um objeto da classe **`JwtService`** que foi criado anteriormente, se for válido então passamos adiante.

  ```java
  if(userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null){
    UserDetails userDetails = this.userDetailsService.loadUserByUsername(userEmail);
    if(jwtService.isTokenValid(jwtToken, userDetails)){
        //....
    }
  }
  ```

- Se o token for válido então criaremos um objeto do tipo **`UsernamePasswordAuthenticationToken`** contendo os detalhes do usuário e suas autoridades. Um objeto **`UsernamePasswordAuthenticationToken`** representa uma tentativa de autenticação bem-sucedida ou em andamento, inclusive um dos métodos na sua classe é **`setAuthenticated`**.

Talvez você se pergunte por mais que o **`UserDetails`** também encapsule os detalhes dos usuários por questões de responsabilidade não é a função do UserDetails representar uma tentativa de autenticação, ele representa apenas os detalhes de um usuário seja lá qual for seu estado(autenticado ou não), mas usamos um UserDetails para criar um UsernamePasswordAuthenticationToken.

```java
if(userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null){
  UserDetails userDetails = this.userDetailsService.loadUserByUsername(userEmail);
  if(jwtService.isTokenValid(jwtToken, userDetails)){
      UsernamePasswordAuthenticationToken authToken =
          new UsernamePasswordAuthenticationToken(
                          userDetails,
                          null,
                          userDetails.getAuthorities());
  }
}
```

O argumento **`null`** que dexei ali representa a credentials do usuário, ou seja a senha, porém como estamos utilizando JWT token então não é necessário passar ela.

Quanto ao **`setDetails`**, com ele nós passamos os detalhes da requisição HTTP do cliente.

```java
authToken.setDetails(new WebAuthenticationDetailsSource()
                  .buildDetails(request));
```
