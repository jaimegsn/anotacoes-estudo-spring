# Dependências e configurações Spring Data JPA

Primeiramente devemos adicionar a dependência `‘Spring Data JPA’` e a dependência do driver do banco que queremos no projeto, por exemplo `‘PostgreSQL Driver’` ou `‘MySQL Driver’`... no pom.xml ou qualquer que seja o gerenciador de dependências, **essas dependências estarão no Spring Initializr**

Depois precisamos configurar o JPA e Hibernate no application.properties ou application.yml:
<br>

---

Configuração do JPA e Hibernate

.properties

```arduino
# Configurações do Hibernate e JPA
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

.yml

```yaml
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

- **`spring.jpa.database-platform`**: especifica o dialeto do Hibernate que deve ser usado para se comunicar com o banco de dados.

- **`spring.jpa.hibernate.ddl-auto`**: define como o Hibernate deve gerenciar o esquema do banco de dados. Neste exemplo, a opção **`update`** indica que o Hibernate deve atualizar o esquema automaticamente com base nas entidades do JPA.

- **`spring.jpa.show-sql`**: ativa o log das instruções SQL geradas pelo Hibernate.

- **`spring.jpa.properties.hibernate.format_sql`**: formata as instruções SQL geradas pelo Hibernate para facilitar a leitura e a depuração.
