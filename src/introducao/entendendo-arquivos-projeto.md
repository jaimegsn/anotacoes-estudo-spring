# Entendendo os Arquivos do Projeto

1. Pasta "src/main/java": Essa é a pasta principal do código-fonte do projeto Spring. Aqui é onde você irá escrever suas classes Java para implementar a lógica de negócios e a funcionalidade da aplicação.

2. Pasta "src/main/resources": Nesta pasta, você pode armazenar arquivos de recursos, como arquivos de configuração, arquivos de propriedades e arquivos de dados que sua aplicação precisa. Esses recursos são acessados durante a execução da aplicação.
    1. Podemos apagar as pastas  "src/main/resources/static" e "src/main/resources/templates" caso esteja em um projeto REST pois eles são para outra arquitetura Spring MVC

3. Arquivo "pom.xml": Este arquivo é o arquivo de configuração do Maven, uma ferramenta de gerenciamento de dependências. Nele, você especifica as dependências do projeto, incluindo o Spring Framework, bem como outras configurações relacionadas ao projeto.

4. Pasta "src/test/java": Essa pasta é usada para escrever testes automatizados para sua aplicação. Aqui você pode criar classes de teste para verificar se a funcionalidade do seu código está correta.

5. Pasta "src/test/resources": Assim como a pasta "src/main/resources", esta pasta contém arquivos de recursos específicos para os testes automatizados.

6. Pasta "target": Esta pasta é gerada automaticamente pelo Maven durante o processo de compilação. Ela armazena os arquivos compilados e os artefatos da aplicação, como arquivo JAR ou WAR.