# Many to Many com dados Extras

Many-to-Many com dados extras pode ser aplicado em qualquer cenário em que haja uma associação entre duas entidades e seja necessário armazenar atributos adicionais específicos da relação.

Esses atributos adicionais podem ser atributos simples e primitivos ou podem ser complexos como Value Objects.

Supondo as entidades `Aluno` e `Curso`, como exemplo teremos um dado extra chamado `Aula`, onde ele é um value object.
    
Criamos uma classe chamada `AulaPK` onde seus atributos serão um id, e as entidades das quais ela está associada, nos atributos dos objetos das entidades colocamos a relação **`@ManyToOne`**, pois `Aluno` e `Curso` possuem muitas aulas e o **`@JoinColum()`** com o nome da chave estrangeira. Nessa classe usamos a anotação **`@Embeddable`**.

É importante deixar essa classe serializavel, para facilitar o tráfego na rede com `implements Serializable`
    
```java
@Embeddable
public class AulaPK implements Serializable{
    private Long id;
    	
    @ManyToOne
    @JoinColumn(name="aluno_id")
    private Aluno aluno;
    
    @ManyToOne
    @JoinColumn(name="curso_id")
    private Curso curso;
}
```
    
Agora sim vamos criar o nosso Value Object Aula, ele também precisa implementar a interface `Serializable`:
    
```java
public class Aula implements Serializable{
    
//Note que a annotation do id é diferente de uma entiddade comum.
    @EmbeddedId
    private AulaPK id;

    private Integer hours;
    
    public Aula(Aluno aluno, Curso curso, Integer hours){
    	id.setAluno(aluno);
    	id.setCurso(curso);
    	this.hours = hours;
    }
    
    public Aluno getAluno(){
    	id.getAluno();
    }
    
    public Curso getCurso(){
    	id.getCurso();
    }
}
```
    
A anotação **`@EmbeddedId`** é usada para indicar que a propriedade "id" é uma chave primária incorporada, e o id é um objeto AulaPK.
    
No construtor da classe Aula, definimos as referências para Aluno e Curso através dos métodos da classe AulaPK.
    
Através dos métodos **`getAluno()`** e **`getCurso()`**, acessamos os objetos Aluno e Curso encapsulados na classe AulaPK.
    
**A entidade que precisa ser salva no banco de dados é a entidade Aula, não a entidade AulaPK.**
