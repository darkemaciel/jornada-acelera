# 🚀 Jornada Acelera – Ambiente de Estudos

Este projeto organiza um **ambiente Docker** para acompanhamento do estudo e execução de dois bootcamps: **SQL** e **dbt**.  
Inclui também um site simples [`index.html`](index.html) para monitoramento do progresso.

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
- HTML (`index.html`)
- Futura integração com Python/dbt

---

## 📂 Estrutura do projeto

---

## ⚡ Subindo o ambiente

```bash
docker compose up -d
docker ps
```
---

## 🔗 Acessos
Serviço     Porta Local 	Link de Acesso
Postgres	5432	        localhost:5432
PGAdmin	    15432	        localhost:15432

Abra index.html para visualizar seu progresso.