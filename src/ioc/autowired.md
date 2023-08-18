# @Autowired

No framework spring temos um mecanismo para fazer injeção de dependência  automaticamente.

Para que o próprio Spring instancie um objeto de uma dependência devemos colocar uma annotation @Autowired em cima da dependência:

```java
@Component
public class TestConfig {
    
    @Autowired
    private MangaRepository mangaRepository;
}
```

Sempre que precisarmos usar algum componente podemos utilizar o @Autowired e pronto o próprio spring se encarrega de criar o objeto dessa dependência, só o que precisamos fazer é utiliza-lo.