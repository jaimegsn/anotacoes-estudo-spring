# One to Many

Na associação muitos-para-um e um-para-muitos, considerando o exemplo das entidades `Aluno` e `Professor`, onde existem vários objetos alunos para a entidade professor, podemos realizar o mapeamento da seguinte forma:

```java
@Entity
public class Aluno implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne
    @JoinColumn(name = "professor_id")
    private Professor professor;
}
```

Na classe Aluno, utilizamos a anotação **`@ManyToOne`** para indicar a associação muitos-para-um com a entidade Professor. Também especificamos a coluna de chave estrangeira através da anotação **`@JoinColumn`**, informando o nome do campo que será a chave estrangeira no banco de dados.


O mapeamento **`@ManyToOne`** no Aluno torna o mapeamento **`@OneToMany`** **opcional** na classe Professor. No entanto, podemos mapear também a associação um-para-muitos na classe Professor, da seguinte maneira:

```java
import com.fasterxml.jackson.annotation.JsonIgnore;

@Entity
public class Professor implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @JsonIgnore
    @OneToMany(mappedBy = "professor")
    private List<Aluno> alunos = new ArrayList<>();
}
```

Na classe Professor, utilizamos a anotação **`@OneToMany`** com o atributo **`@OneToMany(mappedBy=professor)`** para indicar a associação um-para-muitos com a entidade Aluno. Especificamos o nome do atributo/campo que representa a associação no lado oposto, que é o atributo **`"professor"`** na classe Aluno.

A annotation **`@JsonIgnore`** tem que ser colocada em algum dos lados caso ocorra a implementação de mão dupla, ou seja a implementação da associação nas duas classes, isso porque quando esse objeto for traduzido para JSON ao ser chamado na API utilizando Postman por exemplo ficará em loop com um JSON aninhado no outro infinitamente, então precisamos ignorar um lado.

Por padrão o JPA sempre irá mostrar apenas a associação no lado que tem apenas um ou seja apenas o atributo professor da entidade Aluno, porque se for fazer ao contrário teremos um JSON muito grande, vsito que temos diversos alunos na entidade Professor, porém é possivel basta adicionarmos o **`@JsonIgnore`** no atributo de associação **`professor`** na classe Aluno, mas para funcionar precisamos adicionar a seguinte configuração no application.properties : `spring.jpa.open-in-view=true`