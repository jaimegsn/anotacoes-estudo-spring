# Ciclo de vida do Spring Framework

1. Configuração: Na primeira fase, o Spring Boot lê e processa as configurações definidas no arquivo application.properties ou application.yml. Essas configurações incluem detalhes como porta do servidor, conexões de banco de dados, etc.

2. Inicialização do contexto: O Spring Boot cria e inicializa o ApplicationContext, que é uma classe que contém todas as informações necessárias para executar a aplicação, como as classes de configuração e os beans.

3. Criação de Beans: Nesta fase, o Spring Boot cria todos os beans que foram definidos. Esses beans incluem, por exemplo, os objetos responsáveis pela conexão com o banco de dados.

4. Execução da aplicação: Com os beans criados e configurados, o Spring Boot inicia a execução da aplicação, que pode incluir a exposição de APIs REST, processamento de filas, etc.

5. Encerramento da aplicação: Quando a aplicação é encerrada, o Spring Boot realiza algumas tarefas importantes, como fechar conexões com o banco de dados, liberar recursos utilizados e executar as ações definidas nos métodos de shutdown hook.
