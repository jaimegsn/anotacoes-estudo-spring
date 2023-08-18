# Camada de Serviços

A camada de serviços no Spring é uma camada intermediária entre a camada de controle (controllers) e a camada de acesso a dados (repositories). A camada de serviços é responsável por fornecer a lógica de negócios da aplicação, implementando as regras e orquestrando as operações de acesso a dados necessárias para executar essas regras.

Lembrando que precisamos indicar que aquela determinada classe é um service colocando uma annotation `@Service` em cima da classe:

```java
@Service
public class PessoaService {

    @Autowired
    private PessoaRepository pessoaRepository;

    public Pessoa save(Pessoa pessoa){
         return pessoaRepository.save(pessoa);
    }

	public List<Pessoa> findAll(){
		return pessoaRepository.findAll();
	}

	public Pessoa findById(Long id){
		Optional<Pessoa> obj = pessoaRepository.findById(id);
		return obj.get();
    }

	// Lembrando que com Data JPA precisamos pegar a referência daquele objeto
    // não basta criar um objeto semelhante ao que estiver no banco
	public Pessoa replaceName(Pessoa obj, Long id){
		Pessoa pessoa = pessoaRepository.getReferenceById(id);
		pessoa.setNome(obj.getNome());
		return pessoaRepository.save(pessoa);
    }

    public void delete(Long id){
        pessoaRepository.deleteById(id);
    }
}
```
