# Camada de Repositórios

O objetivo dos repositórios Spring é fornecer um conjunto de métodos padronizados e simplificados para realizar operações comuns de acesso aos dados, como salvar, atualizar, excluir e consultar dados em um banco de dados.

Para criar os repositórios no Spring, é necessário criar interfaces que estendem a interface JpaRepository.

Geralmente é recomendado que cada entidade tenha um repositório associado a ela. Isso significa que, para cada entidade mapeada em um banco de dados, você deve criar uma interface de repositório que estenda a interface **`JpaRepository` passando no parâmetros do generics a classe da entidade e o tipo do ID, exemplo:**

```java
import com.example.learning.entities.User;
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {

}
```

Não é necessário criar uma implementação para essa interface pois o Spring Data JPA e JpaRepository já tem uma implementação padrão para essa interface basta estendermos o JpaRepository.

Pronto agora basta instanciarmos um objeto UserRepository e conseguimos realizar operações básicas no banco.

Como por exemplo:

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // Exemplo de uso do repositório para salvar um usuário no banco de dados
    public User saveUser(User user) {
        return userRepository.save(user);
    }

    // Exemplo de uso do repositório para buscar um usuário pelo ID
    public User getUserById(Long id) {
        Optional<User> userOptional = userRepository.findById(id);
        return userOptional.orElse(null);
    }

    // Exemplo de uso do repositório para excluir um usuário do banco de dados
    public void deleteUser(Long id) {
        userRepository.deleteById(id);
    }

    // ... outros métodos de serviço ...
}
```
