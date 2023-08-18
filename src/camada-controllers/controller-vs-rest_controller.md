# @Controller vs @RestController

Para indicarmos ao Spring que uma determinada classe é um controller adicionamos uma annotation **`@Controller`** ou **`@RestController`**.

A anotação **`@Controller`** é usada em aplicações web do tipo MVC para lidar com requisições HTTP e fornecer uma resposta em formato de visualização. Geralmente é usado em conjunto com um template engine, como o Thymeleaf, para renderizar a resposta.

A anotação **`@RestController`** também é usada em uma classe para lidar com requisições HTTP, mas a resposta do controller não é um template de visualização e sim respostas em um formato JSON ou XML.
