# Classe de Configuração

Classes configuração são classes que auxiliam a realizar algumas configurações na aplicação, normalmente são criadas em um pacote separado chamado “configs” por exemplo.

Com elas podemos popular um banco, configurar o banco de dados , realizar configurações de segurança e etc.

Para criarmos uma classe de configuração devemos adicionar a annotation **`@Configuration`**, exemplo:

```java
import org.springframework.context.annotation.Configuration;

@Configuration
public class ClasseDeConfiguracao{
	//...
}
```

Podemos criar também uma configuração específica para um perfil da aplicação (dev, test, prod…), para isso basta colocarmos uma annotation **`@Profile("profile")`** para a classe especificando o perfil desejado, exemplo:

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
@Profile("dev")
public class ClasseDeConfiguracao{
	//... configurações específicas para o perfil dev
}
```

Logo essa classe de configuração funcionará apenas quando o determinado perfil estiver ativo, **`spring.profiles.active="dev"`** (config do arquivo application.properties).
