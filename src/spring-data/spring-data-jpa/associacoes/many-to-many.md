# Many to Many

Nesse tipo de associação vamos levar como exemplo as entidades `Aluno` e `Curso`, `Curso` terá vários alunos e `Aluno` terá vários cursos.

Nas associações OneToMany e ManyToOne nós tinhamos um `@JoinColumn` definindo o atributo de chave estrangeira, porém na relação ManyToMany teremos uma criação de uma tabela para associar as duas entidades com o `@JoinTable`.

Dentro do JoinTable teremos duas chaves estrangeiras para as duas entidades, com `joinColumns = @JoinColumn()` definindo a chave estrangeira da entidade onde estamos implementando e `inverseJoinColumns = @JoinColumn()` definindo a chave estrangeira da outra entidade.

```java
@Entity
public class Aluno implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToMany
    @JoinTable(name = "tb_aluno_curso",
				joinColumns = @JoinColumn(name = "aluno_id"),
				inverseJoinColumns = @JoinColumn(name = "curso_id"))
    private Set<Curso> cursos = new HashSet<>();
}
```

Na outra entidade colocamos um mapeamento da associação que fizemos na primeira entidade

```java
@Entity
public class Curso implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

	@JsonIgnore
    @ManyToMany(mappedBy = "cursos") // Nome da coleção da entidade Aluno
    private Set<Aluno> alunos = new HashSet<>();
}
```

Dentro do ManyToMany colocamos um `mappedBy = nome da coleção onde colocamos a annotation @ManyToMany` na entidade Aluno, que no exemplo é `‘cursos’`.

E devemos colocar a annotation `@JsonIgnore` pois temos uma associação de via dupla e precisamos ignorar um lado.