# Criar Profiles

`spring.profiles.active=test`
A configuração de profile é utilizada para definir diferentes configurações para diferentes ambientes de implantação, como desenvolvimento (dev), teste(test) e produção. Perfis comuns são:

- **`default`**: perfil padrão que é usado se nenhum outro perfil for especificado.
- **`dev`**: usado para ambiente de desenvolvimento.
- **`test`**: usado para ambiente de testes.
- **`prod`**: usado para ambiente de produção.
- Podemos também criar perfis personalizados

```yaml
spring.profiles.active=dev #application.properties

#------------------#

#Application.yml
spring:
	profiles:
		active: dev
```

Com o perfil criado podemos criar um arquivo .properties exclusivo para o perfil que está ativo no momento, exemplo: application-dev.properties no pacote resources

Além disso através da annotation `@Profile` é possível definir que um componente específico funcionará apenas com um determinado perfil ativo.

Exemplo de utilizações:

```java
@Configuration
@Profile("dev")
public class DevConfig {
    // configurações específicas para o perfil dev
}
```
