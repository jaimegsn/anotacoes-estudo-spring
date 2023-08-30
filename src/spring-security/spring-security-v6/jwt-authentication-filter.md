# JwtAuthenticationFilter

Após termos criado o JwtService iremos criar o filtro JwtAuthenticationFilter que irá chamar a validação feita no JwtService, para validar o token. 
Até porque JwtService não têm acesso a request e response, quem tem acesso a isso são os filtros.

