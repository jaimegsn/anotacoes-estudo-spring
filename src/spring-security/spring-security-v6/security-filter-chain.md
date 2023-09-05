# SecurityFilterChain

<!--A configuração do SecurityFilterChain inclui a definição de quais caminhos requerem autenticação, quais caminhos são públicos (não requerem autenticação) e quais filtros de segurança devem ser aplicados em diferentes caminhos.
O SecurityFilterChain não lida diretamente com a autenticação; em vez disso, ele especifica como as solicitações devem ser tratadas antes de chegar ao processo de autenticação.-->

Como já visto anteriormente um objeto **`SecurityFilterChain`** é usado para configurar as regras de segurança para determinados caminhos ou URL's na aplicação. Ele define a forma de como as solicitações HTTP são tratadas em termos de autenticação e autorização.

Esse objeto contém uma série de filtros de segurança que o Spring Security irá utilizar para garantir a autenticação e autorização da aplicação, por isso criaremos um **Bean personalizado** dele para gerenciar e personalizar os filtros da nossa maneira.

Para isso criaremos uma classe de configuração com as seguintes annotations:

- **`@Configuration`**: Indica que essa classe contém configurações específicas para a aplicação.

- **`@EnableWebSecurity`**: Faz parte do Spring Security e é usada para habilitar a configuração de segurança baseada na web. Isso significa que a classe SecurityConfig será responsável por configurar a segurança web da aplicação.

- **`@RequiredArgsConstructor`**: Essa é só se você estiver utilizando Lombok, cria um construtor para variáveis com o modificador 'final'.

Exemplo:

```java
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    //...
}
```

Dentro dessa classe iremos criar o **Bean de `SecurityFilterChain`** que irá proporcionar um objeto **`SecurityFilterChain`** que o Spring Security irá utilizar para aplicar os filtros de segurança:

```java
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception{
        //...
    }
}
```

Com os métodos do objeto **`HttpSecurity http`** no parâmetro nós podemos configurar diversos filtros de segurança:

- **`http.csrf(csrf -> {csrf})`**: com esse método nós definimos a configuração do csrf na nossa aplicação web.

- **`http.authenticationProvider(AuthenticationProvider obj)`**: com esse método, definimos o AuthenticationProvider que é responsável por fornecer a autenticação que será executada, podendo ser (podemos criar um objeto AuthenticationProvider como um bean e deixar o Spring se encarregar de injeta-lo, falaremos sobre a criação desse objeto depois) essa autenticação .

Com este método, você associa um AuthenticationProvider (um mecanismo de autenticação) ao seu SecurityFilterChain. Isso significa que, quando alguém tentar fazer login, o Spring Security usará esse AuthenticationProvider para autenticar o usuário

    - DaoAuthenticationProvider: Usado para autenticar os usuários com base em informações armazenadas em um banco de dados.

    - JwtAuthenticationProvider: Usado para autenticar solicitações com base em tokens JWT (JSON Web Tokens).

- **`http.authorizeHttpRequests(auth -> {auth})`**: com esse método, configuramos as regras de autorização para as solicitações HTTP. É aqui que você pode definir quais caminhos requerem autenticação e quais não requerem, bem como outras regras de autorização.
