# Criando as tabelas utilizando PostgreSQL

### Permission

```sql
CREATE TABLE IF NOT EXISTS "permission" (
  id SERIAL NOT NULL PRIMARY KEY,
  description VARCHAR(255) DEFAULT NULL
);
```

### Users

```sql
CREATE TABLE IF NOT EXISTS "users"(
  id SERIAL NOT NULL PRIMARY KEY,
  user_name VARCHAR(255) UNIQUE DEFAULT NULL,
  full_name VARCHAR(255) DEFAULT NULL,
  password VARCHAR(255) DEFAULT NULL,
  account_non_expired BIT(1) DEFAULT NULL,
  account_non_locked BIT(1) DEFAULT NULL,
  credentials_non_expired BIT(1) DEFAULT NULL,
  enabled BIT(1) DEFAULT NULL
);
```

### User-Permission

```sql
CREATE TABLE IF NOT EXISTS "user_permission" (
  id_user BIGINT NOT NULL,
  id_permission BIGINT NOT NULL,

  FOREIGN KEY (id_user) REFERENCES users(id),
  FOREIGN KEY (id_permission) REFERENCES permission(id)
);
```
