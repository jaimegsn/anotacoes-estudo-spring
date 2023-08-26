# Como se proteger de CSRF, Teoria

O processo básico de proteção contra CSRF no Spring Security é o seguinte:

1. Geração do Token CSRF:
   Quando um usuário se autentica, o Spring Security gera um token CSRF exclusivo para a sessão do usuário. Esse token é gerado aleatoriamente e é associado à sessão do usuário.

2. Envio do Token para o cliente:
   O token gerado é passado para o cliente por meio de cookies, é gerado um cookie seguro de uso único para o cliente na qual é enviado pelo servidor junto com a resposta quando o cliente se autentica, isso é feito automaticamente pelo Spring Security.
   O cookie possui um nome específico, como "XSRF-TOKEN".

3. Inclusão do Token na Requisição:
   Quando é enviado uma requisição de volta ao servidor com potencial para executar ações que modificam o estado do servidor (POST, PUT, DELETE..) o token é incluido na requisição de alguma forma.

REST: em aplicações REST, o valor do cookie é automaticamente incluído na requisição pelo navegador como parte dos cabeçalhos HTTP, geralmente como um cabeçalho chamado "X-XSRF-TOKEN" ou similar.

MVC: em aplicações MVC, o valor do cookie é incluído nos formulários em campos ocultos.

4. Validação do Token:
   O Spring Security verifica se o token CSRF fornecido na requisição corresponde ao token associado à sessão do usuário. Se os tokens não coincidirem, a requisição é considerada potencialmente maliciosa e é rejeitada.

Documentação do Spring sobre: https://docs.spring.io/spring-security/reference/features/exploits/csrf.html
