# Value Object (VO)

O padrão Value Object (Objeto de Valor) é um padrão de design utilizado na programação para representar um objeto complexo mas não possui identidade própria e não é uma entidade.

Por exemplo em uma Entidade Pessoa podemos ter um Value Object chamado `Endereco`, `Endereco` não é uma entidade ele é apenas um **atributo** de `Pessoa`, ou seja um objeto de valor, de caráter informativo que por sua vez possui vários campos como rua, bairro, cep…

Exemplos comuns de Value Objects são datas, moedas, coordenadas geográficas, CPF, entre outros.

Mas como armazenamos isso no banco ? depende da abordagem podemos serializar esse objeto em um JSON ou XML e armazenar em um campo da tabela ou criamos uma nova tabela e nesses casos terá que adicionar um identificador no value object.

**Objetos de valor são imutáveis, ou seja apenas getters na classe e o construtor para setar os campos. Caso precise mudar o objeto de valor faça um novo objeto**

## Implementação:

Abaixo está um exemplo de implementação do Value Object `Endereco`:

```java
public class Endereco {
    private final String rua;
    private final String bairro;
    private final String cep;

    public Endereco(String rua, String bairro, String cep) {
        this.rua = rua;
        this.bairro = bairro;
        this.cep = cep;
    }

    public String getRua() {
        return rua;
    }

    public String getBairro() {
        return bairro;
    }

    public String getCep() {
        return cep;
    }
}

```

Neste exemplo, a classe Endereco é imutável, pois seus atributos são finais e não há setters para alterá-los após a criação do objeto.

Para armazenar o objeto Endereco no banco de dados, podemos seguir duas abordagens comuns:

- Serialização em JSON ou XML: Nessa abordagem, podemos converter o objeto Endereco em formato JSON ou XML e armazená-lo em um campo da tabela relacionada. Para isso, podemos utilizar bibliotecas como Jackson ou Gson para fazer a serialização e desserialização do objeto.

  Exemplo de como armazenar o objeto Endereco em uma entidade Pessoa utilizando a serialização em JSON:

  ```java
  @Entity
  public class Pessoa {
      // outros atributos da entidade

      @Column(columnDefinition = "TEXT")
      private String enderecoJson; // campo para armazenar o endereco em formato JSON

      public void setEndereco(Endereco endereco) {
          this.enderecoJson = new Gson().toJson(endereco);
      }

      public Endereco getEndereco() {
          return new Gson().fromJson(enderecoJson, Endereco.class);
      }
  }

  ```

- Nessa abordagem, a classe Endereco é anotada com `@Embeddable`, indicando que é um componente embutido em outra entidade. A classe Pessoa utiliza o Value Object Endereco através da anotação `@Embedded`.

  Com essa configuração, a tabela de Pessoa terá as colunas correspondentes aos atributos de Endereco (rua, bairro e cep) como se fossem colunas próprias da tabela de Pessoa, sem a necessidade de criar uma tabela separada para o Value Object. Dessa forma, o Endereco será tratado como um componente e será armazenado diretamente na tabela de Pessoa.

  ```java
  @Embeddable
    public class Endereco {
        private String rua;
        private String bairro;
        private String cep;

        // Construtor e getters
    }

    @Entity
    public class Pessoa {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        private String nome;

        @Embedded
        private Endereco endereco;

        // Construtor, getters e setters
    }
  ```
