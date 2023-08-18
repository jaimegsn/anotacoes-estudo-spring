# Limitando endpoints na documentação do Swagger e Redefinindo URL de acesso ao Swagger UI

Limitar a documentação para endpoints especificos é útil quando você tem várias APIs em um mesmo projeto ou contexto, e deseja que o Swagger mostre apenas a documentação da API que você está trabalhando, tornando a visualização mais específica e organizada.
<br>

Fazemos isso através de configurações feitas no arquivo **`application.properties`** ou **`application.yml`**

```yaml
# application.properties
    springdoc.paths-to-match=/api/**/v1/**
    springdoc.swagger-ui.use-root-path=true


# application.yml
    springdoc:
        paths-to-match: /api/**/v1/**
        swagger-ui:
            use-root-path: true
```
<br>

- **`springdoc.paths-to-match`**: Essa configuração é usada para limitar a documentação do Swagger apenas para os endpoints da API que correspondem ao padrão especificado. No exemplo dado (`/api/**/v1/**`).
    <br>
O **`**`** é usado como um coringa usado para representar qualquer sequência de caracteres de qualquer tamanho. Isso significa que pode corresponder a zero caracteres, um caractere, vários caracteres ou mesmo nenhum texto.
  <br>
URLs como **`"/api/users/v1/"`**, **`"/api/products/v1/"`**, etc., seriam incluídas na documentação do Swagger, enquanto URLs que não seguem esse padrão seriam excluídas.

- **`springdoc.swagger-ui.use-root-path`**: Essa configuração é usada para indicar se a interface do Swagger deve ser acessada na raiz do contexto da aplicação. Se definido como "true", a interface do Swagger será disponibilizada na raiz, ou seja, em http://localhost:8080/. Caso contrário, a interface do Swagger ficará disponível em http://localhost:8080/swagger-ui.html, por exemplo.  