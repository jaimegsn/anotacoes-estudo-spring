# Definindo Associações entre as Entidades

As associações são relacionamentos entre as entidades, por exemplo uma entidade `Aluno` terá um atributo `private meuProfessor` do tipo `Professor` nos seus atributos.
<br>

Enquanto a entidade `Professor` terá uma lista como atributo com vários objetos do tipo `Aluno`, por exemplo `private List<Aluno> meusAlunos = new ArrayList<>()`, logo essas duas entidades estão associadas.

Existem diferentes tipos de associação:

- [One to Many e Many to One](./associacoes/one-to-many.md)
- [Many to Many](./associacoes/many-to-many.md)
- [Many to Many com dados extras](./associacoes/many-to-many-dados-extras.md)
