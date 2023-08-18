# Conectando a aplicação com um banco de dados

<details>
<summary>PostgreSQL</summary>
    
---
    
.properties
    
```arduino
# Configurações do banco de dados
spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://localhost:5432/nome_do_banco?createDatabaseIfNotExist=true
spring.datasource.username=usuario
spring.datasource.password=senha
    
# Configurações do Hibernate e JPA
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```
    
.yml
    
```yaml
# Configurações do banco de dados
spring:
    datasource:
    	driver-class-name: org.postgresql.Driver
    	url: jdbc:postgresql://localhost:5432/nome_do_banco?createDatabaseIfNotExist=true
    	username: usuario
    	password: senha
    
# Configurações do Hibernate e JPA
    jpa:
    	database-platform: org.hibernate.dialect.PostgreSQLDialect
    	hibernate:
    		ddl-auto: update
    	show-sql: true
    	properties:
    		hibernate:
    			format_sql: true
```
    
- **`spring.datasource.driver-class-name`**: especifica a classe do driver JDBC a ser usada pelo Spring para se comunicar com o banco de dados.

- **`spring.datasource.url`**: a URL de conexão com o banco de dados, que deve incluir o nome do banco de dados que você deseja usar.

- **`spring.datasource.username`** e **`spring.datasource.password`**: as credenciais de autenticação usadas para acessar o banco de dados.
</details>
<br>
