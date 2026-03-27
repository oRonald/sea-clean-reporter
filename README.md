# Environmental Monitoring API

## Backend para Registro e Gestão de Ocorrências Ambientais

API REST desenvolvida em Java com Spring Boot para gerenciamento de ocorrências ambientais reportadas por usuários, viabilizando a atuação de ONGs e colaboradores na resolução de problemas como acúmulo de resíduos em regiões costeiras e outras degradações ambientais.

## Tecnologias

| Tecnologia                     | Descrição                              |
|------------------------------|----------------------------------------|
| Java 21                      | Linguagem principal                    |
| Spring Boot                  | Framework base da aplicação            |
| Spring Data JPA / Hibernate  | Persistência e mapeamento ORM          |
| Bean Validation              | Validação de dados de entrada          |
| Oracle Database              | Banco de dados relacional              |
| Swagger / OpenAPI            | Documentação dos endpoints             |
| Maven                        | Gerenciamento de dependências          |

## Arquitetura

A aplicação segue o padrão REST com separação em camadas:

## Estrutura do Projeto

| Diretório        | Descrição                                      |
|------------------|----------------------------------------------|
| controller/      | Endpoints REST e recebimento de requisições   |
| service/         | Regras de negócio                             |
| repository/      | Acesso ao banco de dados via JPA              |
| model/           | Entidades e mapeamento ORM                    |
| dto/             | Objetos de transferência de dados             |

## Funcionalidades

- Cadastro e gerenciamento de usuários
- Cadastro e gerenciamento de ONGs
- Associação de usuários a ONGs
- Criação e gestão de reports (ocorrências ambientais)
- Atribuição de colaboradores a reports
- Controle de status de reports (em andamento / concluído)
- Controle de status de colaboradores (ativo / inativo)
- Consulta de contribuições por colaborador

## Endpoints

### Usuários

| Método | Rota                                      | Descrição                     |
|--------|-------------------------------------------|------------------------------|
| POST   | /usuarios                                 | Cadastrar usuário            |
| GET    | /usuarios                                 | Listar usuários              |
| GET    | /usuarios/{id}                            | Detalhes do usuário          |
| PUT    | /usuarios/{id}                            | Atualizar usuário            |
| DELETE | /usuarios/{id}                            | Remover usuário              |
| POST   | /usuarios/{idUsuario}/ong/{idOng}          | Vincular usuário a ONG       |

### Reports (Ocorrências)

| Método | Rota                                  | Descrição                      |
|--------|---------------------------------------|--------------------------------|
| POST   | /usuarios/report/helper/{idHelper}    | Criar report de ocorrência     |
| GET    | /usuarios/report/{idHelper}           | Listar reports do usuário      |
| PUT    | /usuarios/report/end/{id}             | Concluir report                |

### ONGs

| Método | Rota        | Descrição           |
|--------|------------|---------------------|
| POST   | /ongs      | Cadastrar ONG       |
| GET    | /ongs      | Listar ONGs         |
| GET    | /ongs/{id} | Detalhes da ONG     |
| PUT    | /ongs/{id} | Atualizar ONG       |
| DELETE | /ongs/{id} | Remover ONG         |

### Colaboradores

| Método | Rota                                           | Descrição                              |
|--------|-----------------------------------------------|----------------------------------------|
| GET    | /colaboradores                                | Listar colaboradores ativos            |
| GET    | /colaboradores/inativos                       | Listar colaboradores inativos          |
| GET    | /colaboradores/{id}/contribuicoes             | Ver contribuições do colaborador       |
| PUT    | /colaboradores/{id}/report/{idReport}         | Atribuir report ao colaborador         |
| DELETE | /colaboradores/{id}/inativo                   | Marcar colaborador como inativo        |

## Como rodar o projeto

### Pré-requisitos
- Java 21
- Maven
- Oracle Database (ou ajuste o application.properties para H2 em memória para testes)

````
# 1. Clone o repositório
git clone https://github.com/seu-usuario/seu-repositorio.git

# 2. Acesse a pasta do projeto
cd environmental-monitoring-api

# 3. Configure o banco de dados em src/main/resources/application.properties
spring.datasource.url=jdbc:oracle:thin:@localhost:1521:xe
spring.datasource.username=SEU_USUARIO
spring.datasource.password=SUA_SENHA

# 4. Execute a aplicação
mvn spring-boot:run
````
Acessando a documentação Swagger
````
http://localhost:8080/swagger-ui/index.html
````

### Regras de Negócio

- Usuários podem criar reports de ocorrências ambientais
- Reports podem ser atribuídos a colaboradores para resolução
- Reports concluídos são registrados no histórico de contribuições do colaborador
- Colaboradores podem ser marcados como inativos sem remoção do histórico
- Usuários podem ser vinculados a ONGs para atuação coordenada

#### Projeto desenvolvido na FIAP com foco na aplicação prática de conceitos de backend: arquitetura em camadas, persistência com ORM, validação de dados e design de APIs REST.
