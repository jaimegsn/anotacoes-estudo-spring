# Entendendo o que é Cross-Site Request Forgery (CSRF)

CSRF ou XSRF, é um tipo de ataque cibernético em que um invasor tenta enganar um usuário autenticado para que ele execute ações não intencionais em um sistema online no qual o usuário está autenticado. 

O ataque ocorre quando o invasor consegue fazer com que o navegador do usuário envie solicitações HTTP legítimas, mas não autorizadas, para um aplicativo da web.

O principal objetivo do ataque CSRF é explorar a confiança do sistema no navegador do usuário. 

Ao aproveitar a autenticação do usuário no aplicativo, o atacante pode induzir o usuário a realizar ações indesejadas, como alterar configurações, fazer compras, excluir informações ou realizar outras operações sensíveis, sem o conhecimento ou consentimento do usuário autenticado.

Aqui está uma descrição mais detalhada de como funciona um ataque CSRF:

1. **Usuário Autenticado**: O usuário autenticado está conectado a um aplicativo da web legítimo em um navegador.

2. **Página Maliciosa**: O invasor cria uma página web maliciosa que contém código que gera uma solicitação HTTP para uma ação sensível no aplicativo alvo. Isso pode ser feito por meio de formulários ocultos ou chamadas de JavaScript.

3. **Engano do Usuário**: O invasor engana o usuário para que ele acesse a página maliciosa. Isso pode ser feito por meio de técnicas como phishing, compartilhamento de links enganosos ou outros métodos.

4. **Solicitação Não Intencional**: O código na página maliciosa faz com que o navegador do usuário envie uma solicitação HTTP legítima para uma ação sensível no aplicativo alvo. Como o usuário já está autenticado no aplicativo, o servidor trata a solicitação como se fosse legítima.

5. **Ação Não Autorizada**: A solicitação é processada pelo servidor do aplicativo e realiza uma ação não autorizada, como alterar informações do usuário, efetuar transações ou executar outras operações.

Esses ataques têm sucesso porque não é possível diferenciar uma requisição vinda de alguma origem maliciosa de uma origem legitima, então é necessário ter algo na origem legitima que não possa existir na origem maliciosa, para que seja possível diferenciar as duas requisições.