# Criando as entidades User e Permission

### User:

```java
@Entity
@Table(name = "users")
public class User implements Serializable, UserDetails {
    public User(){

    }

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "user_name")
    private String userName;
    @Column(name = "full_name")
    private String fullName;
    @Column
    private String password;
    @Column(name = "account_non_expired")
    private Boolean accountNonExpired;
    @Column(name = "account_non_locked")
    private Boolean accountNonLocked;
    @Column(name = "credentials_non_expired")
    private Boolean credentialsNonExpired;

    @Column
    private Boolean enabled;

    @ManyToMany(fetch = FetchType.EAGER)
    @JoinTable(name="user_permission",
    joinColumns = @JoinColumn(name="id_user"),
    inverseJoinColumns = @JoinColumn(name = "id_permission"))
    private List<Permission> permissions;

    public List<String> getRoles(){
        List<String> roles = new ArrayList<>();
        for (Permission p : this.permissions) {
            roles.add(p.getDescription());
        }
        return roles;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return this.permissions;
    }

    @Override
    public String getPassword() {
        return this.password;
    }

    @Override
    public String getUsername() {
        return this.userName;
    }

    @Override
    public boolean isAccountNonExpired() {
        return this.accountNonExpired;
    }

    @Override
    public boolean isAccountNonLocked() {
        return this.accountNonLocked;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return this.credentialsNonExpired;
    }

    @Override
    public boolean isEnabled() {
        return this.enabled;
    }

/*
Setters, Getters, Hashcode and Equals
 */

```


### Permission:

```java
@Entity
@Table(name = "permission")
public class Permission implements Serializable, GrantedAuthority {
    public Permission(){

    }

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column
    private String description;


    @Override
    public String getAuthority() {
        return description;
    }

    /*
    Getters, Setters, Hashcode and Equals...
     */

```