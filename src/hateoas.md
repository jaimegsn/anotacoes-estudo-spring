# Implementando HATEOAS

Hypermedia as the Engine of Application State (HATEOAS) é um conceito fundamental para tornar uma API RESTful. Trata-se de adicionar links ou referências a outros endpoints dentro da API, permitindo que o cliente navegue e acesse recursos relacionados.
Isso significa que o cliente pode descobrir e interagir com outros recursos da API de forma dinâmica, com base nas informações fornecidas pelos links.

### Dependência:

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-hateoas</artifactId>
</dependency>
```

## Herdando a classe RepresentationModel<T> no objeto DTO

Para implementar o HATEOAS, em nossa API, precisamos herdar a classe **`RepresentationModel<T>`** da biblioteca HATEOAS na nossa classe DTO.

Essa classe terá recursos onde conseguiremos passar links para outros endpoints.

```java
public class PersonDTO extends RepresentationModel<PersonDTO> implements Serializable
```

## Preparando o objeto DTO na camada de serviços ou controller

Na camada de serviços ou controller, podemos utilizar o método **`add()`** da classe **`RepresentationModel`** para adicionar um link no nosso objeto DTO.

No entanto esse link não pode ser apenas uma String, ele precisa ser dinâmico e representar uma URI, para isso, usamos os método da classe WebMvcLinkBuilder que nos ajudarão a construir um link dinâmico.

Um desses métodos é o **`linkTo()`**, que espera receber como parâmetro algum link.

```java
PersonDTO p = ...;
p.add(WebMvcLinkBuilder.linkTo());
```

## Adicionando a referência do Link

Antes de adicionarmos o parâmetro no método linkTo(), por questões de visualização é interessante primeiro eu mostrar como adicionar para onde o link está se referenciando. Para isso temos alguns métodos:

```java
PersonDTO p = ...;
p.add(WebMvcLinkBuilder.linkTo().withRel("Listagem de pessoas"))// com string
p.add(WebMvcLinkBuilder.linkTo().withSelfRel())// o proprio objeto em si
```

## Adicionando o Link:

Precisamos adicionar o link de forma dinâmica para suportar alterações na url e não de forma estática, então para isso apontaremos para algum método do Controller, assim mudanças na url não fará diferença.

Para isso utilizaremos o método **`methodOn()`** que receberá como parâmetro a classe do controller(Controller.class), seguido da chamada do método.

```java
PersonDTO p = ...;
p.add(linkto(WebMvcLinkBuilder.methodOn(PersonController.class).findAll())
						).withRel("Listagem de pessoas");
```

Podemos passar diversos links dentro do método **`.add()`**
