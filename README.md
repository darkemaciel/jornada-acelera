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

```bash
docker compose up -d
docker ps
```
---

## Introdução

Bem-vindos ao nosso workshop sobre SQL e PostgreSQL. Hoje, vamos mergulhar nos conceitos básicos de bancos de dados e como o PostgreSQL pode ser utilizado para gerenciar dados de forma eficiente. Nosso objetivo é garantir que todos vocês tenham uma boa base para explorar mais sobre SQL e operações de banco de dados nos próximos dias.

## Por que Postgres?

PostgreSQL é um sistema de gerenciamento de banco de dados relacional (RDBMS) desenvolvido no Departamento de Ciência da Computação da Universidade da Califórnia em Berkeley. POSTGRES foi pioneiro em muitos conceitos que só se tornaram disponíveis em alguns sistemas de banco de dados comerciais muito mais tarde:

* complex queries
* foreign keys
* triggers
* updatable views
* transactional integrity

Além disso, o PostgreSQL pode ser estendido pelo usuário de várias maneiras, por exemplo, adicionando novos

* data types
* functions
* operators
* aggregate functions
* index methods
* procedural languages

## Informações Adicionais 

Além do conteúdo do curso, recomendo alguns outros lugares para estudo.

[Documentação](https://www.postgresql.org/docs/current/index.html) Documentação oficial do Postgres, todas as features estão aqui.


[Wiki](https://wiki.postgresql.org/wiki/Main_Page) A wiki do PostgreSQL contém a lista de Perguntas Frequentes (FAQ), lista de tarefas pendentes (TODO) e informações detalhadas sobre muitos outros tópicos.

[Site](https://www.postgresql.org/) na Web O site do PostgreSQL fornece detalhes sobre a última versão e outras informações para tornar seu trabalho ou lazer com o PostgreSQL mais produtivo.

[Comunidade](https://github.com/postgres/postgres) O código O PostgreSQL é um projeto de código aberto. Como tal, depende da comunidade de usuários para suporte contínuo. À medida que você começa a usar o PostgreSQL, dependerá de outros para obter ajuda, seja através da documentação ou através das listas de discussão. Considere devolver o seu conhecimento. Leia as listas de discussão e responda às perguntas. Se você aprender algo que não está na documentação, escreva e contribua com isso. Se você adicionar recursos ao código, contribua com eles.

## Instalação

Antes de poder usar o PostgreSQL, você precisa instalá-lo, é claro. É possível que o PostgreSQL já esteja instalado em seu local, seja porque foi incluído na distribuição do seu sistema operacional ou porque o administrador do sistema já o instalou.

Se você não tem certeza se o PostgreSQL já está disponível ou se você pode usá-lo para suas experimentações, então você pode instalá-lo por conta própria. Fazer isso não é difícil e pode ser um bom exercício.

- Instalando o postgres Local

## Fundamentos da Arquitetura

Antes de prosseguirmos, é importante que você entenda a arquitetura básica do sistema PostgreSQL. Compreender como as partes do PostgreSQL interagem tornará tudo mais fácil.

No jargão de tecnologia, o PostgreSQL utiliza um modelo cliente/servidor. 

Um processo servidor, que gerencia os arquivos de banco de dados, aceita conexões com o banco de dados de aplicações cliente e executa ações no banco de dados em nome dos clientes. O programa do servidor de banco de dados é chamado de postgres.

A aplicação cliente do usuário (frontend) que deseja realizar operações de banco de dados. As aplicações cliente podem ser muito diversas em natureza: um cliente pode ser uma ferramenta orientada a texto, uma aplicação gráfica, um servidor web que acessa o banco de dados para exibir páginas web ou uma ferramenta especializada de manutenção de banco de dados. Algumas aplicações cliente são fornecidas com a distribuição do PostgreSQL; a maioria é desenvolvida pelos usuários.

Como é típico em aplicações cliente/servidor, o cliente e o servidor podem estar em hosts diferentes. Nesse caso, eles se comunicam por uma conexão de rede TCP/IP. Você deve ter isso em mente, porque os arquivos que podem ser acessados em uma máquina cliente podem não ser acessíveis (ou podem ser acessíveis apenas com um nome de arquivo diferente) na máquina do servidor de banco de dados.

O servidor PostgreSQL pode lidar com múltiplas conexões simultâneas de clientes. Para alcançar isso, ele inicia (“forks”) um novo processo para cada conexão. A partir desse ponto, o cliente e o novo processo servidor se comunicam sem intervenção do processo postgres original. Assim, o processo servidor supervisor está sempre em execução, aguardando conexões de clientes, enquanto os processos de clientes e servidores associados vêm e vão. (Tudo isso, é claro, é invisível para o usuário. Só mencionamos isso aqui para completude.)

## Criando um Banco de Dados

O primeiro teste para verificar se você pode acessar o servidor de banco de dados é tentar criar um banco de dados. Um servidor PostgreSQL em execução pode gerenciar vários bancos de dados. Tipicamente, um banco de dados separado é usado para cada projeto ou usuário.

Para isso vamos entrar dentro do nosso cliente `pgAdmin 4`

Também podemos nos conectar em servidores remoto, ex: `Render`

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

