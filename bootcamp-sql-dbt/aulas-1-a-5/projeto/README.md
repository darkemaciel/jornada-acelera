# 🚀 Jornada Acelera – Ambiente de Estudos

Este projeto organiza um **ambiente Docker** para acompanhamento do estudo e execução do bootcamp: **SQL**.

---

## 🐳 Status do Docker

![Docker](https://img.shields.io/badge/Docker-OK-brightgreen)
![Postgres](https://img.shields.io/badge/Postgres-Running-brightgreen)
![PGAdmin](https://img.shields.io/badge/PGAdmin-Running-brightgreen)

> ⚠️ Os badges são ilustrativos; confirme status real via `docker ps`.

---

## 🛠 Tecnologias

- Docker & Docker Compose
- Postgres
- PGAdmin

---

## ⚡ Subindo o ambiente

### Manualmente

Utilize o arquivo SQL fornecido, `nortwhind.sql`, para popular o seu banco de dados.

### Com Docker e Docker Compose

**Pré-requisito**: Instale o Docker e Docker Compose

* [Começar com Docker](https://www.docker.com/get-started)
* [Instalar Docker Compose](https://docs.docker.com/compose/install/)

### Passos para configuração com Docker:

1. **Iniciar o Docker Compose** Execute o comando abaixo para subir os serviços:
    
    ```
    docker-compose up -d
    ```
    
    Aguarde as mensagens de configuração, como:
    
    ```csharp
    Creating network "northwind_psql_db" with driver "bridge"
    Creating volume "northwind_psql_db" with default driver
    Creating volume "northwind_psql_pgadmin" with default driver
    Creating pgadmin ... done
    Creating db      ... done
    ```
       
2. **Conectar o PgAdmin** Acesse o PgAdmin pelo URL: [http://localhost:15432](http://localhost:15432), com a senha `postgres`. 

Configure um novo servidor no PgAdmin:
    
    * **General**:
        * Name: Docker
    * **Connection**:
        * Host name/address: postgres
        * Port: 5432
        * Maintenance database: docker
        * Nome de usuário: docker
        * password: postgres


## Introdução

Bem-vindos ao nosso workshop sobre SQL e PostgreSQL. Hoje, vamos mergulhar nos conceitos básicos de bancos de dados e como o PostgreSQL pode ser utilizado para gerenciar dados de forma eficiente. Nosso objetivo é garantir que todos vocês tenham uma boa base para explorar mais sobre SQL e operações de banco de dados nos próximos dias.



## Fundamentos da Arquitetura

Antes de prosseguirmos, é importante que você entenda a arquitetura básica do sistema PostgreSQL. Compreender como as partes do PostgreSQL interagem tornará tudo mais fácil.

No jargão de tecnologia, o PostgreSQL utiliza um modelo cliente/servidor. 

Um processo servidor, que gerencia os arquivos de banco de dados, aceita conexões com o banco de dados de aplicações cliente e executa ações no banco de dados em nome dos clientes. O programa do servidor de banco de dados é chamado de postgres.

A aplicação cliente do usuário (frontend) que deseja realizar operações de banco de dados. As aplicações cliente podem ser muito diversas em natureza: um cliente pode ser uma ferramenta orientada a texto, uma aplicação gráfica, um servidor web que acessa o banco de dados para exibir páginas web ou uma ferramenta especializada de manutenção de banco de dados. Algumas aplicações cliente são fornecidas com a distribuição do PostgreSQL; a maioria é desenvolvida pelos usuários.

Como é típico em aplicações cliente/servidor, o cliente e o servidor podem estar em hosts diferentes. Nesse caso, eles se comunicam por uma conexão de rede TCP/IP. Você deve ter isso em mente, porque os arquivos que podem ser acessados em uma máquina cliente podem não ser acessíveis (ou podem ser acessíveis apenas com um nome de arquivo diferente) na máquina do servidor de banco de dados.

O servidor PostgreSQL pode lidar com múltiplas conexões simultâneas de clientes. Para alcançar isso, ele inicia (“forks”) um novo processo para cada conexão. A partir desse ponto, o cliente e o novo processo servidor se comunicam sem intervenção do processo postgres original. Assim, o processo servidor supervisor está sempre em execução, aguardando conexões de clientes, enquanto os processos de clientes e servidores associados vêm e vão. (Tudo isso, é claro, é invisível para o usuário. Só mencionamos isso aqui para completude.)


## Criando nosso Schema

![Northwind database](https://github.com/pthom/northwind_psql/raw/master/ER.png)

Para este projeto, vamos utilizar um script SQL simples que preencherá um banco de dados com o famoso exemplo [Northwind](https://github.com/pthom/northwind_psql), adaptado para o PostgreSQL. Esse script configurará o banco de dados Northwind no PostgreSQL, criando todas as tabelas necessárias e inserindo dados de exemplo para que você possa começar a trabalhar imediatamente com consultas e análises SQL em um contexto prático. Este banco de dados de exemplo é uma ótima ferramenta para aprender e praticar as operações e técnicas de SQL, especialmente útil para entender como manipular dados relacionais em um ambiente realista.

## Primeiros comandos

Vamos agora para um guia introdutório para operações básicas de SQL utilizando o banco de dados Northwind. Cada comando SQL será explicado com uma breve introdução para ajudar no entendimento e aplicação prática.

#### Exemplo de Seleção Completa

Para selecionar todos os dados de uma tabela:

```sql
-- Exibe todos os registros da tabela Customers
SELECT * FROM customers;
```

#### Seleção de Colunas Específicas

Para selecionar colunas específicas:

```sql
-- Exibe o nome de contato e a cidade dos clientes
SELECT contact_name, city FROM customers;
```

#### Utilizando DISTINCT

Para selecionar valores distintos:

```sql
-- Lista todos os países dos clientes
SELECT country FROM customers;
-- Lista os países sem repetição
SELECT DISTINCT country FROM customers;
-- Conta quantos países únicos existem
SELECT COUNT(DISTINCT country) FROM customers;
```

#### Cláusula WHERE

Para filtrar registros:

```sql
-- Seleciona todos os clientes do México
SELECT * FROM customers WHERE country='Mexico';
-- Seleciona clientes com ID específico
SELECT * FROM customers WHERE customer_id='ANATR';
-- Utiliza AND para múltiplos critérios
SELECT * FROM customers WHERE country='Germany' AND city='Berlin';
-- Utiliza OR para mais de uma cidade
SELECT * FROM customers WHERE city='Berlin' OR city='Aachen';
-- Utiliza NOT para excluir a Alemanha
SELECT * FROM customers WHERE country<>'Germany';
-- Combina AND, OR e NOT
SELECT * FROM customers WHERE country='Germany' AND (city='Berlin' OR city='Aachen');
-- Exclui clientes da Alemanha e EUA
SELECT * FROM customers WHERE country<>'Germany' AND country<>'USA';
```

#### ORDER BY

Para ordenar os resultados:

```sql
-- Ordena clientes pelo país
SELECT * FROM customers ORDER BY country;
-- Ordena por país em ordem descendente
SELECT * FROM customers ORDER BY country DESC;
-- Ordena por país e nome do contato
SELECT * FROM customers ORDER BY country, contact_name;
-- Ordena por país em ordem ascendente e nome em ordem descendente
SELECT * FROM customers ORDER BY country ASC, contact_name DESC;
```

#### Utilizando LIKE e IN
Para busca por padrões e listas de valores:

```sql
-- Clientes com nome de contato começando por "a"
SELECT * FROM customers WHERE contact_name LIKE 'a%';
-- Clientes com nome de contato não começando por "a"
SELECT * FROM customers WHERE contact_name NOT LIKE 'a%';
-- Clientes de países específicos
SELECT * FROM customers WHERE country IN ('Germany', 'France', 'UK');
-- Clientes não localizados em 'Germany', 'France', 'UK'
SELECT * FROM customers WHERE country NOT IN ('Germany', 'France', 'UK');
```
---
