# Explicando Arquitetura do Spring Security 6

Acho melhor explicar 3 fluxos, o Login/Autenticação, Register e executar alguma operação na API/Autorização.

### Login/Autenticação

1. O processo começa com uma requisição enviada pelo cliente para o endpoint de login, por exemplo **'auth/login'**, essa requisição vem acompanhado de um objeto DTO que normalmente tem o usuário e a senha, esse DTO pode ter o nome por exemplo de **`AccountCredentialsDTO`**.

2. Essa requisição passa por uma série de filtros de segurança (SecurityFilterChain), esses filtros aplicam checagens de segurança com base nas configurações pré-definidas no Bean do objeto **`SecurityFilterChain`**. Se os requisitos não forem atendidos, exceções como **"UNAUTHORIZED"** ou **"FORBIDDEN"** podem ser lançadas, os filtros de segurança possuem acesso tanto à request quanto à response durante a comunicação cliente-servidor.

3. Um desses filtros de segurança que pode ser aplicado é o **`JWTAuthenticationFilter`**, ele intercepta a requisição do cliente e verifica se um JWT Válido foi enviado junto, se o token não for encontrado a autenticação é rejeitada. Esse é um filtro que não existe nativamente no Spring Security, então para aplicar ele precisamos cria-lo, ele será uma classe irá estender a classe abstrata **`OncePerRequestFilter`**.

4. **`OncePerRequestFilter`** é uma classe abstrata fornecida pelo Spring que foi projetada para ser estendida ao criar filtros personalizados no contexto Spring Security, em particular essa classe é executado apenas uma vez por solicitação, independente quantas vezes **`SecurityFilterChain`** seja invocado. **`OncePerRequestFilter`** exige que seja implementado o método doFilterInternal que é o método onde aplicamos a lógica do filtro de segurança.

5. **`JwtService`** , após uma verificação básica inicial do **`JWTAuthenticationFilter`** apenas para saber se o token é um token JWT, precisamos agora validar se o token JWT é realmente um token válido e para isso criaremos um **`JwtService`** que será responsável por lidar com a criação, validação e gerenciamento de tokens JWT, essa classe encapsula a lógica necessária para trabalhar com JWTs, permitindo que outros componentes da aplicação interajam com eles de maneira mais simples e organizada. As responsabiliddades do **`JwtService`**, podem incluir:

   - Criação de Tokens JWT
   - Validação de Tokens
   - Extração de dados do token
   - Renovação do Token
   - Revogação do Token

   asdas

6. Após a requisição passar por todos os filtros de segurança e chegar ao controller da aplicação, é criado um objeto do tipo **`UsernamePasswordAuthenticationToken`** com o usuário e senha do DTO que chegou na requisição, esse objeto será utilizado pelo AuthenticationManager para o processo de autenticação subsequente.

7. O **`AuthenticationManager`** coordena o processo de autenticação, ele é responsável por executar uma lista de "provider"(provedor) para a autenticação. Cada provedor faz uma certa verificação, AuthenticationManager é uma interface e a classe mais comum utilizada que implementa ela é a ProviderManager

8. Existe um provedor chamado **`DaoAuthenticationProvider`**, ele é responsável por verificar se existe aquele usuário no banco e se as senhas coincidem, lembrando que não podemos salvar a senha real no banco como uma String, é preciso criptografar ela, o **`DaoAuthenticationProvider`** utilizará um objeto **`PasswordEncoder`** para esse processo de criptografar a senha do DTO e comparar com a do banco, mas para isso precisamos criar um bean de **`PasswordEncoder`**.

9. Enquanto o **`DaoAuthenticationProvider`**, faz a validação, o objeto que de fato faz a busca do usuário no banco de dados é o **`UserDetailsService`**, ele é uma interface que precisamos implementar em um service comum que podemos criar e dar o nome que quiser, **`UserDetailsService`** terá apenas um método que é o de busca e ele retorna um objeto **`UserDetails`**, contendo as informações do usuário que ele buscou no banco.

10.

5 - JWTAuthenticationProvidder, ele é outro provider

6 - Caso a JWTAuthenticationFilter exista na aplicação e obtenha um sucesso é gerado um SecurityContextHolder, caso ela falhe
