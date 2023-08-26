# JWT ou token transparente vs Token opaco

Bom primeiramente devemos nos perguntar se precisamos transmitir dados sensíveis utilizando o token, se sim é recomendado utilizar-se de tokens opaco, caso não pode-se usar um token transparente como o JWT, é até possível combinar os dois nesse caso.

A vantagem do JWT é que não precisamos armazenar o Token no banco de dados, diferente do token opaco já que é uma string aleatória ele precisa estar vinculado a alguma informação no banco de dados, para consulta posteriormente.

# JWT vs Token Opaco: Qual escolher?

Ao escolher entre JWT (JSON Web Token) e tokens opacos, é importante considerar a natureza dos dados que serão transmitidos e os requisitos específicos do seu sistema. Abaixo estão algumas considerações a serem feitas:

1. Sensibilidade dos Dados:
   - Se você precisa transmitir dados sensíveis no token, é recomendado usar tokens opacos. Isso ocorre porque os tokens opacos não armazenam informações no token, tornando os dados menos suscetíveis a exposição.

2. Transparência vs. Opacidade:
   - Tokens opacos ocultam os detalhes internos do token e armazenam as informações relevantes no servidor de autenticação (Banco de dados). Eles são úteis quando você não quer que os detalhes do token sejam acessíveis externamente.
   - JWTs são transparentes, pois contêm informações legíveis e autocontidas no próprio token. Essas informações são protegidas por assinatura ou criptografia.

3. Vantagens do JWT:
   - Não é necessário consultar o banco de dados para validar um JWT, pois a assinatura contida no próprio token pode ser verificada.
   - Isso melhora o desempenho, reduzindo as chamadas ao banco de dados durante a validação.
   - Os JWTs podem ser úteis para autenticação entre serviços ou microsserviços, onde a validação eficiente é essencial.

4. Vantagens dos Tokens Opacos:
   - Dados sensíveis não são expostos externamente, fornecendo uma camada adicional de segurança.
   - Aumenta a capacidade de revogação, já que o servidor de autenticação pode invalidar um token semelhante ao uso de sessões.

5. Combinando Ambos:
   - Em alguns casos, pode ser benéfico combinar os dois tipos de tokens. Por exemplo, você pode usar JWTs para autenticação entre serviços e tokens opacos para autenticação de usuários.

Lembre-se de que a escolha entre JWT e tokens opacos depende das necessidades do seu sistema, dos requisitos de segurança e das práticas recomendadas da sua plataforma de desenvolvimento. Avalie cuidadosamente e escolha o método que melhor atenda às suas necessidades de autenticação e autorização.
