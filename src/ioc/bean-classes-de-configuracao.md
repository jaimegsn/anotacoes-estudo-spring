# @Bean em classes de configuração

A anotação **`@Bean`** pode ser usada apenas em métodos de classes anotadas com **`@Configuration`**. Isso significa que você só pode criar beans personalizados em uma classe de configuração.

Apenas com **`@Autowired`**, e sem definir o **`@Bean`** O Spring tentaria encontrar uma instância do componente padrão correspondente no contexto de aplicação e a injetaria onde necessário.

Já utilizando **`@Bean`**, você está explicitamente definindo e configurando a instância do bean que o Spring irá injetar. Dessa forma, você tem mais controle sobre a criação e configuração do bean, permitindo uma maior personalização.

Quando você define um bean usando **`@Bean`**, o Spring o registra no contexto de aplicação e o torna disponível para ser injetado em outras classes que dependem dele.

Vamos supor que você tenha a classe de configuração **`AppConfig`** com um método que cria o bean:

```java
@Configuration
public class AppConfig {

    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

E em outra classe, você quer usar esse bean criado:

```java
@Service
public class MyService {

    private final MyBean myBean;

    @Autowired
    public MyService(MyBean myBean) {
        this.myBean = myBean;
    }

    // ... outros métodos da classe ...
}
```
