# Data Transfer Object (DTO)

"DTO" significa "Data Transfer Object" e é um padrão de design de software amplamente utilizado para transferir dados entre diferentes camadas da aplicação ou entre sistemas distintos. Seu objetivo é garantir uma transferência eficiente de dados, com segurança e redução do tráfego em sistemas web.

Na prática, criamos uma classe DTO que possui uma estrutura semelhante à da entidade correspondente. Por exemplo, se temos uma entidade chamada `"Pessoa"`, criamos a classe `"PessoaDTO"` que contém apenas os atributos e informações necessárias para a transferência de dados. Em geral, alguns atributos irrelevantes para o processo em questão e são excluídos do DTO.

Vamos supor que chegue uma requisição do cliente para cadastrar uma pessoa irá vir um objeto `PessoaDTO`, o objeto é enviado para a camada de serviço. Lá, ocorre a conversão desse DTO em um objeto do tipo `"Pessoa"`, que é então persistido no banco de dados. Após a conclusão do processo, o objeto `Pessoa` é convertido novamente em `PessoaDTO` e retornado ao controller, fornecendo a informação de que a pessoa foi devidamente cadastrada.

Essa abordagem permite controlar quais informações são transmitidas e evita a exposição de dados desnecessários. Além disso, a conversão entre DTO e entidade auxilia na separação de responsabilidades entre as camadas da aplicação, melhorando a segurança e o desempenho geral do sistema.

### Implementação:

- [Conversão na mão](./dto/na-mao.md)
- Utilizando Bibliotecas

  Fazer o processo de conversão de objetos entre entidade e um DTO ao longo do tempo ficará massivo e trabalhoso além de suscetível a erros, então para isso temos bibliotecas em Java que fazem esse trabalho por nós:

  - [MapStruct](./dto/mapStruct.md)
