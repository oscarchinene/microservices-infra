
# 🐳 Infraestrutura - Docker Compose

Este repositório é responsável por orquestrar todos os microserviços do **MyMicroservice** usando Docker Compose.

Todos os microserviços serão inicializados e registrados automaticamente no Eureka, permitindo rodar o sistema completo localmente sem precisar configurar cada microserviço individualmente.

---

## 🚀 Serviços incluídos

| Serviço                | Porta  | Descrição                         |
|------------------------|--------|----------------------------------|
| config-server          | 8888   | Config Server                    |
| service-main           | 8888   | Eureka + Config Server           |
| service-notification   | 8082   | Envio de notificações            |
| service-tasks          | 8081   | Gerenciamento de tarefas         |

---

## 📦 Executando todos os serviços

```bash
cd infra
docker-compose up --build
```

- Todos os serviços serão iniciados e registrados automaticamente no Eureka.

- Permite rodar localmente o sistema completo sem configurar cada microserviço individualmente.

## 🌐 URLs úteis

- Eureka Dashboard: http://localhost:8888/eureka

- H2 Console (Service Tasks): http://localhost:8081/h2-console

## 📄 Descrição dos serviços
1️⃣ Config Server

- Centraliza todas as configurações (service-notification.properties, service-tasks.properties)

- Porta: 8888

- Endpoint de configuração: /config


2️⃣ Service Main

- Microserviço principal que funciona como Config Server + Eureka Server

- Porta: 8888


3️⃣ Service Notification

- Recebe notificações via endpoint POST /notification

- Porta: 8082

- Dependência: Config Server (service-main)

- Registro no Eureka (service-main)

4️⃣ Service Tasks

- Gerencia tarefas e envia notificações para tarefas próximas do prazo

- Porta: 8081

- Endpoints:

- GET /message → retorna mensagem do Config Server

- POST /tasks → cria uma nova tarefa

## Banco de dados: H2 em memória

- URL: jdbc:h2:mem:testdb

- Console: http://localhost:8081/h2-console

- Usuário: sa, senha: (vazia)

- Tabela principal: tasks

- Dependências: Config Server e Service Notification
