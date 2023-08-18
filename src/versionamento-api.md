# Versionamento da API

À medida que os sistemas evoluem, é comum adicionar novas funcionalidades, modificar comportamentos ou remover recursos. O versionamento é uma prática que permite fazer essas alterações de forma controlada, mantendo a compatibilidade com versões anteriores e oferecendo flexibilidade aos consumidores da API para adotar ou migrar para versões mais recentes, conforme necessário.

Existem diferentes abordagens para realizar o versionamento de uma WEB API, sendo três delas comumente usadas: path params, query params e subdomínio. Vamos entender cada uma delas:

1. **Path Params**: Nessa abordagem, a versão da API é incluída diretamente na URL como parte do caminho (path). Por exemplo: `https://api.example.com/v1/users` (versão 1) e `https://api.example.com/v2/users` (versão 2). Essa abordagem é simples e amplamente adotada, permitindo a diferenciação dos endpoints da API para cada versão.
2. **Query Params**: Nessa abordagem, a versão da API é passada como um parâmetro de consulta (query parameter) na URL. Por exemplo: `https://api.example.com/users?version=1` (versão 1) e `https://api.example.com/users?version=2` (versão 2). É necessário interpretar o parâmetro da consulta no servidor para rotear a solicitação para a versão apropriada da API.
3. **Subdomínio**: Nessa abordagem, a versão da API é indicada através de um subdomínio na URL. Por exemplo: `https://v1.api.example.com/users` (versão 1) e `https://v2.api.example.com/users` (versão 2). Essa abordagem separa claramente as diferentes versões da API em subdomínios distintos.

É importante destacar que não há uma abordagem única e correta para o versionamento de APIs. A escolha entre path params, query params ou subdomínio dependerá das necessidades específicas do sistema e das convenções adotadas pela equipe de desenvolvimento.

O objetivo é estabelecer um padrão claro e consistente para o versionamento, comunicando adequadamente aos consumidores da API sobre as versões disponíveis e os eventuais impactos nas atualizações.

---
### Versionando a API utilizando Path Params:

1. Na camada de DTO temos os objetos que trafegam nas requisições, então é importante previamente separa-los em versões de pacotes diferentes, por exemplo: dto.v1.*;  e  dto.v2.*; 
Dentro de cada versão do pacote DTO, definimos os objetos DTO’s que precisamos como “PersonDTOV1” e “PersonDTOV2”. Cada versão pode adicionar ou remover recursos conforme a necessidade.
2. Podemos adotar duas estratégias comuns na camada de controller.  
A primeira é criar uma nova classe controller específica para a versão desejada, separado por pacotes, como "controllers.v1" e "controllers.v2".
A segunda é versionar apenas as operações em si, ou seja, criar novos métodos no controller já existente.
3. Na camada de service segue o mesmo pensamento.
Podemos criar nova classes Services, omo "services.v1" e "services.v2”.
Ou podemos apenas criar novos métodos.
4. Também é necessário criar um novo Mapper para realizar a conversão dos novos DTO’s, ou criar novos métodos com o Mapper já existente.