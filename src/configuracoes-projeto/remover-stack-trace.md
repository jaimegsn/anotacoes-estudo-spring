# Remover stack trace do endpoint caso haja algum erro

.properties:

```arduino
server.error.include-stacktrace=always  #Padrão, sempre será mostrado
server.error.include-stacktrace=never  #Nunca será mostrado
server.error.include-stacktrace=on_param  #exibe se colocarmos o (?trace=true) na url
```

.yml:

```yaml
server:
	error:
		include-stacktrace: always # always, never, on_param
```