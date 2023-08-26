# Implementando JWT Provider

Iremos primeiramente criar uma classe **`seuprojeto.com.securityJwt.JwtTokenProvider.java`**
dentro dessa classe irá ter o seguinte código:

Em application.properties iremos fazer a seguinte configuração:
### Properties:
```yml
#properties:

# Quanto tempo o nosso token irá durar ? em ms
security.jwt.token.expire-length: 3600000

#Secret key:
security.jwt.token.secret-key: 53cr37
```

### YML:
```yml
#YML:


security:
    jwt:
        token:
            secret-key: 53cr37 # Secret key
            expire-length: 3600000 # Quanto tempo o nosso token irá durar ? em ms

```