# my-knowledge-about-spring-framework

Anotações sobre o framework Spring enquanto estudo sobre ele

## ROADMAP:

- [Introdução](./src/introducao.md)
  - [Preparando Ambiente](./src/introducao/preparando-ambiente.md)
  - [Criando projeto com Spring Initializr](./src/introducao/criando-projeto-spring-initializr.md)
  - [Padrão Camadas](./src/introducao/padrao-camadas.md)
  - [Entendendo os Arquivos do Projeto](./src/introducao/entendendo-arquivos-projeto.md)
- [Camada de Controllers](./src/camada-de-controllers.md)
  - [@Controller vs @RestController](./src/camada-controllers/controller-vs-rest_controller.md)
  - [Métodos ou verbos HTTP nos controllers](./src/camada-controllers/metodos-http-controllers.md)
    - [@RequestMapping](./src/camada-controllers/metodos-http-controllers/request-mapping.md)
    - [@GetMapping, @PostMapping, @PutMapping, @DeleteMapping](./src/camada-controllers/metodos-http-controllers/get-post-put-delete-mapping.md)
    - [Produces e Consumes](./src/camada-controllers/metodos-http-controllers/produces-consumes.md)
    - [Melhorando o Produces e Consumes](./src/camada-controllers/metodos-http-controllers/melhorando-produces-consumes.md)
  - [Parâmetros](./src/camada-controllers/parametros.md)
    - [Path Params, (”/users/1”)](./src/camada-controllers/parametros/path-params.md)
    - [Query ou Request Params, (”?q=termo&pagina=2”))](./src/camada-controllers/parametros/request-params.md)
    - [Data Binding](./src/camada-controllers/parametros/data-binding.md)
    - [Request Body](./src/camada-controllers/parametros/request-body.md)
  - [Resposta personalizada com ResponseEntity](./src/camada-controllers/response-entity.md)
- [IoC, Injeção de Dependências, Componentes e Bean](./src/ioc.md)
  - [Injeção de dependências no Java Puro](./src/ioc/java-puro.md)
  - [@Autowired](./src/ioc/autowired.md)
  - [Injeção de dependências com Construtor](./src/ioc/construtor.md)
  - [@Autowired em cada atributo vs @Autowired com Construtor](./src/ioc/autowired-vs-construtor.md)
  - [Componentes Spring](./src/ioc/componentes.md)
  - [Bean](./src/ioc/bean.md)
  - [@Bean em classes de configuração](./src/ioc/bean-classes-de-configuracao.md)
- [Ciclo de vida do Spring Framework](./src/ciclo-vida-spring-framework.md)
- [Camada de Serviços](./src/camada-servicos.md)



## Mdbook

Antes certifique-se de instalar corretamente o mdBook seguindo o guia de instalação: [GUIA de Instalação](https://rust-lang.github.io/mdBook/guide/installation.html)

Para realizar o build do projeto em livro você pode utilizar a ferramenta [mdbook](https://rust-lang.github.io/mdBook/). Assim fica mais fácil a leitura e você pode exportar até mesmo para o kindle. 


Para isso, baixe o repositório e use um dos comandos abaixo:

```sh
$ mdbook build
```

Para subir o livro localmente use:

```sh
$ mdbook serve
```
