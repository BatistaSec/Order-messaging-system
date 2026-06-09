# 🚀 Order Processing System

## 📌 Sobre o projeto

Sistema distribuído de processamento de pedidos baseado em arquitetura de microserviços e comunicação assíncrona utilizando RabbitMQ.

O projeto simula um fluxo real de e-commerce, onde pedidos são criados em um serviço principal e eventos são enviados de forma assíncrona para outro serviço responsável pelo processamento e envio de notificações.

A aplicação também conta com autenticação e autorização utilizando JWT (JSON Web Token), garantindo segurança no acesso às rotas protegidas.

---

## 🧠 Tecnologias utilizadas

* Java 17
* Spring Boot
* Spring Data JPA
* Spring Security
* JWT (JSON Web Token)
* RabbitMQ
* Spring AMQP
* Swagger / OpenAPI
* MySQL
* Maven

---

## 🧱 Arquitetura do sistema

O sistema é composto por dois microserviços independentes:

### 🟦 Order Service

Responsável por:

* Autenticação com JWT
* Criação de pedidos
* Persistência no MySQL
* Publicação de eventos no RabbitMQ

---

### 🟩 Notification Service

Responsável por:

* Consumo de eventos do RabbitMQ
* Processamento de mensagens
* Simulação de envio de notificações

---

### 🔄 Fluxo da aplicação

```text
Usuário → Order Service → MySQL
                     ↓
                RabbitMQ
                     ↓
        Notification Service
                     ↓
        Processamento da notificação
```

### 🔐 Autenticação

* A aplicação utiliza autenticação baseada em JWT (JSON Web Token).

* Para obter o token de acesso, é necessário realizar login com credenciais válidas.

###  👤 Usuário de teste (ambiente de desenvolvimento)
    {
       "username": "admin",
       "password": "admin123"
    }
### 📌 Como obter o token
#### POST /auth/login

    Exemplo de request:

    {
      "username": "admin",
      "password": "admin123"
    }

    Exemplo de response:

    {
      "token": "eyJhbGciOiJIUzI1NiJ9..."
    }
### 🔒 Uso do token

* O token deve ser enviado no header das requisições protegidas:

* Authorization: Bearer SEU_TOKEN
* ❌ Credenciais inválidas

* Se o usuário ou senha estiverem incorretos, a API retornará erro de autenticação.

### 📚 Documentação da API

#### A documentação está disponível via Swagger UI:

* http://localhost:8080/swagger-ui/index.html
#### 📌 Exemplo de evento enviado
     {
       "orderId": 1,
       "customerName": "João",
       "total": 250.00,
       "createdAt": "2026-06-09T10:30:00"
     }
### 📂 Estrutura do projeto
#### Order Service
```text
src/main/java/com/order/
├── controller
├── service
├── repository
├── entity
├── dto
├── security
├── producer
├── config
└── exception
```
#### Notification Service
``` text
src/main/java/com/notification/
├── consumer
├── service
├── config
└── dto
```
### ▶️ Como executar o projeto
#### 1. Clonar os repositórios
      git clone https://github.com/BatistaSec/order-service
      git clone https://github.com/BatistaSec/notification-service
#### 2. Criar banco de dados
     CREATE DATABASE orders_db;
#### 3. Subir o RabbitMQ (Docker)
      docker run -d --name rabbitmq \
      -p 5672:5672 \
      -p 15672:15672 \
      rabbitmq:3-management
#### 4. Configurar application.properties
        spring.datasource.url=jdbc:mysql://localhost:3306/orders_db
        spring.datasource.username=root
        spring.datasource.password=senha

        spring.jpa.hibernate.ddl-auto=update
        spring.jpa.show-sql=true
       
        spring.rabbitmq.host=localhost
        spring.rabbitmq.port=5672
        spring.rabbitmq.username=guest
        spring.rabbitmq.password=guest
       
#### 5. Executar a aplicação
      mvn spring-boot:run

* Execute primeiro o Gestao_de_Pedidos e depois o Service.

### 🧪 Testando o sistema

#### Você pode testar a aplicação utilizando:

* Swagger UI
* Postman
* RabbitMQ Management UI

### 📊 Melhorias futuras
* 🐳 Dockerização completa do sistema
* 🔁 DLQ (Dead Letter Queue)
* 🔄 Retry automático de mensagens
* 🧾 Versionamento de eventos (V1 / V2)
* 🧠 Saga Pattern (fluxo de pagamento)
* 📊 Correlation ID para rastreamento de logs
* 📡 Observabilidade e métricas 
### 👨‍💻 Autor

João Batista

GitHub: https://github.com/BatistaSec
