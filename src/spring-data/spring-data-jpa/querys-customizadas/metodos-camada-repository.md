# Métodos personalizados na camada de repositórios

Utilizando essa abordagem, criaremos métodos personalizados na camada de repositórios e o Spring Data JPA irá analisas o nome do método e, com base nele, gera a consulta SQL correspondente para recuperar os dados do banco de dados.

Por isso o nome do método precisa atender a certos padrões, ele deve começar com **`findBy`**, seguido do nome do(s) campo(s) que servirá(ão) como filtro(s), o nome dos campos no método precisam ser iguais aos dos campos no objeto(entidade). Exemplo: **`findByName(String n)`**, o tipo dos parâmetros precisam ser iguais aos dos campos também, porém o nome do parâmetro pode ser qualquer um.

**O tipo de retorno do método caso não seja uma busca por id ou algum campo único será sempre uma lista**

Podemos fazer várias consultas com vários campos, lembrando que a ordem dos campos importa na pesquisa, aqui vai uma variedade:

1. findByNome: Isso recuperará os registros que possuem o atributo **`nome`** exatamente igual ao valor fornecido.

2. findByNomeContaining: Isso recuperará os registros que possuem o atributo **`nome`** que contenha a substring fornecida. É útil para pesquisas parciais.

3. findByNomeIgnoreCase: Isso recuperará os registros que possuem o atributo **`nome`** que seja igual ao valor fornecido, ignorando maiúsculas e minúsculas.

4. findByNomeOrderByDataNascimentoDesc: Isso recuperará os registros que possuem o atributo **`nome`** exatamente igual ao valor fornecido e retornará os resultados ordenados por **`dataNascimento`** em ordem decrescente.

5. findByNomeOrEmail: Isso recuperará os registros que possuem o atributo **`nome`** exatamente igual ao valor fornecido ou o atributo **`email`** exatamente igual ao valor fornecido. É uma consulta com múltiplos critérios usando a palavra-chave "Or".

6. findByDataCadastroBetween: Isso recuperará os registros que possuem o atributo **`dataCadastro`** dentro de um determinado intervalo.

7. findByAtivoTrue: Isso recuperará os registros que possuem o atributo **`ativo`** com valor igual a **`true`**.

8. findByNomeIsNull: Isso recuperará os registros que possuem o atributo **`nome`** com valor nulo.

9. findByNomeIsNotNull: Isso recuperará os registros que possuem o atributo **`nome`** com valor não nulo.

10. findByNomeIgnoreCaseAndIdadeGreaterThan: Isso recuperará os registros que possuem o atributo **`nome`** igual ao valor fornecido, ignorando maiúsculas e minúsculas, e com o atributo **`idade`** maior que o valor fornecido. É uma consulta com múltiplos critérios usando a palavra-chave "And".

Exemplo em código:

```java
@Repository
public interface PlanetRepository extends JpaRepository<Planet, Long> {

    public Optional<List<Planet>> findByName(String txt);

    public List<Planet> findByTerrainContainsAndClimateContains(String t, String c);

}
```
