# Evolutionary Database Design e Migrations

## Evolutionary Database Design:

O Evolutionary Database Design é uma filosofia ou abordagem que reconhece a necessidade de evolução e adaptação dos bancos de dados ao longo do tempo. Ele promove a ideia de que os bancos de dados devem ser projetados e evoluídos incrementalmente, acompanhando as mudanças nos requisitos do sistema.

## Migrations:

Migrations é um conceito que está diretamente relacionado a filosofia Evolutionary Database Design, ele têm a ideia de versionar o esquema do banco de dados registrando todas as alterações feitas ao longo do tempo sendo possível reverter para versões anteriores do banco de dados se necessário.

As migrations são arquivos que contêm instruções e comandos para realizar alterações no esquema do banco de dados, cada arquivo de migração representa uma versão específica do banco de dados, e esses arquivos são organizados de forma sequencial, permitindo que as alterações sejam aplicadas em ordem cronológica.

Aqui estão ferramentas ou bibliotecas que implementam o conceito de migrations:

- [FlyWay](./spring-data-jpa/migrations/flyway.md)
