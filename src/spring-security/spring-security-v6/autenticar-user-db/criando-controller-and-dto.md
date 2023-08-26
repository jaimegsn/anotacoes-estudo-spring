# Criando DTO's

Precisamos criar um Controller que irá ser responsável por receber requisições do Client para realizar autenticação.

Quando se trata de autenticação, é geralmente uma prática recomendada usar o método POST para enviar credenciais de autenticação, o motivo principal é que os dados enviados via POST são incluídos no corpo da requisição HTTP, o que torna mais difícil para terceiros interceptarem esses dados em comparação com o método GET, onde os parâmetros são anexados à URL.

### Controller

```java


```


Também precisamos criar um DTO que esse Controller irá receber, normalmente o DTO irá conter apenas o username e password.

### AccountCredentialsDTO

```java
public class AccountCredentialsDTO implements Serializable {
    private String username;
    private String password;

    public AccountCredentialsDTO(){}

    public AccountCredentialsDTO(String username, String password){
        this.username=username;
        this.password=password;
    }

    /*
    getters,setter, hashcode and equals..
    */
}
```



### TokenDTO

```java
public class TokenDTO implements Serializable {
    private String username;
    private Boolean authenticated;
    private Date created;
    private Date expiration;
    private String accessToken;
    private String refreshToken;

    public TokenDTO(){}

    public TokenDTO(String username,
                    Boolean authenticated,
                    Date created,
                    Date expiration,
                    String accessToken,
                    String refreshToken) {

        this.username = username;
        this.authenticated = authenticated;
        this.created = created;
        this.expiration = expiration;
        this.accessToken = accessToken;
        this.refreshToken = refreshToken;
    }

   /*
    Getters,setters,hashcod and equals..
    */
}

```