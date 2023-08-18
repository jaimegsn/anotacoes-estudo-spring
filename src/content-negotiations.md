# Content Negotiations (API em XML, YAML.. e Internacionalização)

Content Negotiation é a capacidade da aplicação REST ser mais flexível e adaptável, permitindo que diferentes clientes recebam o conteúdo em formatos (JSON, XML, YML, CSV…) e idiomas compatíveis com suas preferências, o que melhora a experiência do usuário e a interoperabilidade da aplicação.

## Dependências:

Link para as dependências https://mvnrepository.com/artifact/com.fasterxml.jackson.dataformat

Precisamos adicionar algumas dependências para prover o conteúdo em outros formatos:

- XML

  ```xml
  <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.dataformat/jackson-dataformat-xml -->
  <dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
  </dependency>
  ```

- YML

  ```xml
  <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.dataformat/jackson-dataformat-yaml -->
  <dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-yaml</artifactId>
  </dependency>
  ```
