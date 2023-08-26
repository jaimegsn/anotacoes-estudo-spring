# Personalizando a autenticação básica em memória

Sabendo que o Spring Security V6 utiliza o Bean de **`SecurityFilterChain`** e **`InMemoryUserDetailsManager`**, podemos criar nossos próprios Beans desses dois objetos personalizando-os.

Para isso iremos criar nossa classe de configuração → **`config.SecurityConfig.java`** 

Na classe utilizaremos a annotation **`@EnableWebSecurity`** , ao usar essa annotation você está ativando o módulo de segurança do Spring e informando ao Spring Framework que essa classe será responsável por fornecer as configurações de segurança específicas para a aplicação.

```java
@EnableWebSecurity
@Configuration
public class SecurityConfig {

    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        http.authorizeHttpRequests((authz) -> authz.anyRequest().authenticated());
        http.formLogin(Customizer.withDefaults());
        http.httpBasic(Customizer.withDefaults());
        return http.build();
    }

		@Bean
    public InMemoryUserDetailsManager userDetailsService() {
        PasswordEncoder passwordEncoder = PasswordEncoderFactories.createDelegatingPasswordEncoder();
        UserDetails user = User.withUsername("user")
                .password(passwordEncoder.encode("123"))
                .roles("USER")
                .build();

        return new InMemoryUserDetailsManager(user);
    }
}
```

Aqui vai a lógica utilizada no userDetailsService:

- Para gerarmos uma senha mais segura e não uma **`String`**, utilizaremos o tipo **`PasswordEncoder`**.

- O usuário será criado com métodos estáticos da classe **`USER`** que ao final executará **`build()`** e retornará um **`UserDetails`**.

- Ao final retornamos um objeto **`InMemoryUserDetailsManager`** que irá receber como parâmetro o user.