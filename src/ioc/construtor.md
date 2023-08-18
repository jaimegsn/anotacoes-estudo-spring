# Injeção de dependências com Construtor

Podemos também criar um construtor para as dependências que o proprio Spring se encarregará de gerenciar a  injeção das dependências:

```java
@Component
public class Test{

    private MangaRepository mangaRepository;

    @Autowired
	public Test( MangaRepository mangaRepository){
		this.mangaRepository = mangaRepository;
	}
}
```

É recomendado utilizar a anotação @Autowired mesmo quando a injeção de dependências é realizada pelo construtor, ao utilizar a anotação @Autowired no construtor, você está seguindo uma das melhores práticas recomendadas pelo Spring para realizar a injeção de dependências. Isso torna o código mais legível, facilita a realização de testes unitários e ajuda a evitar dependências não inicializadas.