# FlyWay

Site: [https://flywaydb.org](https://flywaydb.org/)

Primeiramente precisamos adicionar o FlyWay como dependência no pom.xml:

```xml
Verificar se não mudou a forma de colocar a dependência no Spring Initialzr.

<dependency>
	<groupId>org.flywaydb</groupId>
	<artifactId>flyway-core</artifactId>
</dependency>
```

- Os arquivos migrations ficarão no seguinte diretório: “src/main/resources/db/migration”
- Os arquivos migrations podem ser escritos em sql, kotlin ou java; particulamente gosto de utilizar a sintaxe sql.
- Temos algumas regras na criação de arquivos migrations para a sintaxe sql, são elas:
    - **Prefixo**: `V` para versionar ([configurable](https://flywaydb.org/documentation/configuration/parameters/sqlMigrationPrefix)), `U` for undo ([configurable](https://flywaydb.org/documentation/configuration/parameters/undoSqlMigrationPrefix)) and `R` for repeatable migrations ([configurable](https://flywaydb.org/documentation/configuration/parameters/repeatableSqlMigrationPrefix))
    - **Versão**: Version with dots or underscores separate as many parts as you like (Not for repeatable migrations)
    - **Separador**: `__` (two underscores) ([configurable](https://flywaydb.org/documentation/configuration/parameters/sqlMigrationSeparator))
    - **Descrição**: Underscores or spaces separate the words
    - **Sufixo**: `.sql`
    - Exemplos: V2__Add_New_Table.sql; U2__Add_New_Table.sql; R__Add_New_Table.sql
    - Um arquivo não pode ter a mesma versão que outro, se eles fazem parte da mesma “versão” use V1.1, V1.2…
- Configuramos o ddl_auto no application.properties ou yml como none, para evitar que o hibernate fique alteranado a estrutura do banco, alteraremos o banco agora apenas com FlyWay
    
    ```yaml
    jpa:
    	hibernate:
    		ddl-auto: none
    ```
    
- Exemplo de arquivo Migration, chamado V1.1__Create_Table_Person.sql:
    
    ```sql
    CREATE TABLE IF NOT EXISTS "person" (
        id SERIAL NOT NULL PRIMARY KEY,
        first_name VARCHAR(80) NOT NULL,
        last_name VARCHAR(80) NOT NULL,
        address VARCHAR(100) NOT NULL,
        gender VARCHAR(6) NOT NULL
    );
    ```
    

o Flyway cria uma tabela de histórico das migrações chamada "flyway_schema_history". Essa tabela registra todas as migrações que foram executadas no banco de dados. Cada migração é identificada no campo "checksum" onde é armazenado um código hash dos arquivos de migração. Esse código hash é usado pelo Flyway para verificar se os arquivos foram modificados desde a última execução. Se o código hash dos arquivos for diferente do valor armazenado no campo "checksum", o Flyway identifica que houve uma alteração nos arquivos e pode lançar um erro ou tomar ação apropriada, dependendo da configuração.

Então uma minima alteração no arquivo como espaço ou caractere já altera o código hash e ele pode lançar um erro pois o código hash do arquivo mudou e ele não está conseguindo encontrar mais o arquivo que corresponde ao hash do banco, ele tratará o arquivo com uma mudança acidental como um arquivo novo e com um novo hash.

Outra dica é parar o programa ao criar um arquivo migration já que se aquele arquivo for salvo sem querer e o flyway executar ele, ele ficará salvo na tabela “flyway_schema_history” com um código hash e ainda possivelmente em um estado incompleto, caso isso acontece pare a aplicação e apague o ultimo registro da tabela “flyway_shcema_history” e finalize seu arquivo migration.