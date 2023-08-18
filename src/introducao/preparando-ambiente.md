# Preparando Ambiente

<details>
<summary>Windows</summary>

---

1. Instalar alguma JDK (Java Development Kit), como por exemplo da Amazon, Oracle e etc. de alguma versão estável (LTS).

2. Se não houver adicionar uma nova variável de ambiente JAVA_HOME com o caminho para o JDK (C:\Program Files\Java\JDK-17), depois vá para a variável de ambiente PATH, vá em editar e adicione: %JAVA_HOME%\bin

3. java -version; verifica no terminal se o JDK está instalado.

4. Baixar o Apache Maven, pois ele será o nosso gerenciador de dependências. https://maven.apache.org/download.cgi , baixar o: apache-maven-X.X.X-bin.zip, extrair e jogar na pasta arquivos de programas.

5. Em um processo semelhante ao da JDK criaremos uma variável de ambiente chamada M2_HOME com o caminho para a pasta do maven (C:\Program Files\Maven), depois vá para a variável de ambiente PATH, vá em editar e adicione: %M2_HOME%\bin

6. mvn -v; verifica no terminal se o maven está instalado.
7. Instale alguma IDE, como IntelliJ ou Eclipse com Spring tool suite (ele vai baixar um jar que para extrair precisa executar o comando java -jar .\caminho\arquivo.jar)
8. Precisamos baixar e intalar o GIT e configura-lo: https://git-scm.com/downloads

9. Baixar e instalar o PostgreSQL

10. Baixar e instalar o HeidiSQL, é um visualizador de banco de dados leve e de código aberto, desenvolvido para facilitar a administração e gerenciamento de bancos de dados MySQL, MariaDB, Microsoft SQL Server e PostgreSQL. https://www.heidisql.com/download.php

11. Baixar instalar o Postman

12. Baixar e instalar o Docker

</details>
<br>

<details>
<summary>Linux*</summary>

---

</details>
