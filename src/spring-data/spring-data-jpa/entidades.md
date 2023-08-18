# Criando entidades

Uma entidade, no contexto do Spring Data JPA, é uma classe que representa um objeto de negócio ou uma tabela no banco de dados. Ela possui atributos que representam os campos ou colunas da tabela e métodos que definem o comportamento da entidade.

Através do Spring Data JPA, podemos mapear uma entidade para uma tabela no banco de dados de forma automática e transparente. Isso significa que não precisamos escrever consultas SQL manualmente para interagir com o banco de dados, pois o JPA (Java Persistence API) realiza o mapeamento entre a estrutura da entidade e a estrutura da tabela.

## Passos para criar uma Entidade:

1. Colocar a annotation `@Entity` na classe, podemos personalizar como será seu nome na tabela com a annotation `@Table(name=”nome_tabela”)`, caso não queria o nome será igual ao da classe.

2. Definir atributos básicos e colocar a annotation `@Column` em cada um com exceção do ID, na annotation podemos configurar algumas propriedades como tamanho do campo na tabela, podemos personalizar como será o nome do campo na tabela, se ele pode ser nulo e etc..

   - Exemplo: `@Column(name = "first_name", nullable = false, length = 80)` todas essas configurações são opcionais e se quisermos poderíamos ter nenhuma.

   - Podemos alterar também o formato do JSON de um determinado atributo com a annotation @JsonFormat():

   ```java
   import com.fasterxml.jackson.annotation.JsonFormat;

   @JsonFormat(shape = JsonFormat.Shape.STRING,
       pattern = "yyyy-MM-dd'T'HH:mm:ss'Z'",
       timezone = "GMT")
   private LocalDateTime createdat;
   ```

3. Colocar as seguntes annotations no ID: `@Id` e `@GeneratedValue(strategy = GenerationType.IDENTITY)`, que definirá a estratégia de incrementação do ID.

4. Definir as suas associações

5. Necessário criar um construtor vazio para a ORM do Spring e caso queira pode sobrecarregar com mais construtores

   1. O ORM do Spring cria as entidades a partir do resultado da consulta ao banco de dados, o ORM usa o construtor vazio para criar uma instância da classe e em seguida preenche os atributos da entidade com os valores das colunas da tabela correspondente no banco de dados.

6. Criar Getters & Setters, `@Data` com lombok

7. Sobrescrever HashCode e Equals, `@Data` com lombok

8. Implementar a interface serializable para que o objeto possa ser transformado em uma cadeia de bytes para trafegar na rede ao implementar o serializable precisamos adicionar o número de serie:

   `private static final long serialVersionUID = 1L;`

9.

Exemplo:

```java
@Entity
@Table(name = "person")
public class Person implements Serializable {
    public Person() {
    }

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "first_name", nullable = false, length = 80)
    private String firstName;

    @Column(name = "last_name", nullable = false, length = 80)
    private String lastName;

    @Column(nullable = false, length = 100)
    private String address;

    @Column(nullable = false, length = 6)
    private String gender;
}
```
