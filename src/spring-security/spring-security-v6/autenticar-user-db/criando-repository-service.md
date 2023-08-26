# Criando repository e o service

### Repository:

No repository iremos implementar um método que ira consultar registros de usuários no banco baseado no username, poderia ser email também, mas a finalidade dessa consulta é durante o login verificar se o usuário existe e posteriormente comparar se a senha está correta.

```java
@Repository
public interface UserRepository extends JpaRepository<Long, User> {

    @Query("SELECT u FROM User WHERE u.userName =:userName")
    User findByUsername(@Param("userName") String userName);
}
```

---

O UserDetailsService é uma interface específica do Spring Security que faz parte de sua estrutura de autenticação, o Spring Security utiliza o UserDetailsService para buscar os detalhes do usuário correspondente ao nome de usuário fornecido. Esses detalhes incluem principalmente a senha armazenada e as autorizações associadas ao usuário.

Então é necessário que criemos um service que implemente UserDetailService, porque o Spring Security espera receber esse tipo de objeto na sua autenticação, não podemos criar um service comum, pois a interface já possui um método no seu contrato que o Spring Security pretende utilizar, só precisamos sobrescreve-lo.

É o método **`loadUserByUsername(String username)`**, dentro desse método iremos chamar o método do repository

### Service:
```java
@Service
public class UserService implements UserDetailsService {
    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository){
        this.userRepository = userRepository;
    }

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username);
        if(user!=null){
            return user;
        }else{
            throw new UsernameNotFoundException("Username " + username + " Not Found");
        }
    }
}
```

Note que no service nós implementamos a interface **`UserDetailsService`**
