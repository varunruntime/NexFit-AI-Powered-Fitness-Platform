# 🏋️ NexFit — AI-Powered Fitness Application

An **AI-powered fitness application** built using **Spring Boot, React, and Microservices Architecture**. Nexfit allows users to track their fitness activities and receive personalized recommendations powered by **Google Gemini AI**.

The project demonstrates a complete full-stack microservices ecosystem including service discovery, API Gateway, authentication, asynchronous communication, centralized configuration, and AI integration.

---

## 🚀 Features

* 🏃 **Fitness Activity Tracking**
* 🤖 **AI-Powered Fitness Recommendations**
* 🔐 **Secure Authentication & Authorization**
* 👤 **User Management**
* 🌐 **API Gateway**
* 🔎 **Microservice Discovery with Eureka**
* 🐇 **Asynchronous Communication using RabbitMQ**
* ⚡ **Synchronous Inter-Service Communication**
* 🔑 **OAuth 2.0 + PKCE Authentication**
* 🛡️ **Keycloak Integration**
* ⚙️ **Centralized Configuration with Spring Cloud Config**
* 💻 **Modern React Frontend**
* 🗄️ **Database Integration**
* 🔄 **End-to-End Microservices Architecture**

---

## 🏗️ Architecture

FitNova follows a **microservices architecture**, where different responsibilities are separated into independent services.

```text
                    ┌─────────────────────┐
                    │     React Frontend  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     API Gateway     │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       ┌────────────┐   ┌────────────┐   ┌────────────┐
       │   User     │   │  Activity  │   │ AI Service │
       │  Service   │   │  Service   │   │            │
       └─────┬──────┘   └─────┬──────┘   └─────┬──────┘
             │                │                │
             ▼                ▼                ▼
          Database         Database        Gemini API
                              │
                              ▼
                        ┌───────────┐
                        │ RabbitMQ  │
                        └───────────┘

              ┌──────────────────────────┐
              │      Eureka Server       │
              │   Service Discovery      │
              └──────────────────────────┘

              ┌──────────────────────────┐
              │    Config Server         │
              │ Centralized Configuration│
              └──────────────────────────┘

              ┌──────────────────────────┐
              │        Keycloak          │
              │ Authentication & OAuth2  │
              └──────────────────────────┘
```

---

## 🧩 Microservices

### 👤 User Service

Responsible for:

* User registration and management
* User profile information
* Integration with Keycloak user identity
* User-related API endpoints

### 🏃 Activity Service

Responsible for:

* Recording fitness activities
* Storing activity information
* Retrieving activity history
* Sending activity data for AI processing

### 🤖 AI Service

Responsible for:

* Processing fitness activity data
* Communicating with Google Gemini API
* Generating personalized recommendations
* Processing and storing AI-generated recommendations

### 🌐 API Gateway

Acts as the single entry point for frontend requests.

Responsibilities include:

* Routing requests to microservices
* Authentication
* Request filtering
* Service communication

### 🔎 Eureka Server

Provides **service discovery**, allowing microservices to dynamically discover and communicate with each other.

### ⚙️ Config Server

Provides centralized configuration management for all microservices.

### 🐇 RabbitMQ

Used for **asynchronous communication** between services, particularly for sending fitness activity data to the AI service.

### 🔐 Keycloak

Handles:

* User authentication
* Authorization
* OAuth 2.0
* PKCE authentication flow
* Securing APIs

---

## 🤖 AI Integration

FitNova integrates **Google Gemini API** to provide AI-driven fitness recommendations.

The general flow is:

```text
User records activity
        ↓
Activity Service
        ↓
RabbitMQ
        ↓
AI Service
        ↓
Google Gemini API
        ↓
AI-generated recommendation
        ↓
Recommendation stored
        ↓
User receives recommendation
```

This allows AI processing to happen asynchronously without blocking the main activity request.

---

## 🛠️ Tech Stack

### Backend

* Java
* Spring Boot
* Spring Cloud
* Spring Data JPA
* Spring Cloud Gateway
* Spring Cloud Netflix Eureka
* Spring Cloud Config
* Spring Security
* Spring AMQP

### Frontend

* React
* JavaScript
* Redux
* HTML
* CSS

### Database

* PostgreSQL / MySQL

### Messaging

* RabbitMQ

### Authentication

* Keycloak
* OAuth 2.0
* PKCE

### AI

* Google Gemini API

---

## 📁 Project Structure

```text
FitNova/
│
├── user-service/
│   └── Spring Boot application
│
├── activity-service/
│   └── Spring Boot application
│
├── ai-service/
│   └── Spring Boot application
│
├── eureka-server/
│   └── Service discovery
│
├── api-gateway/
│   └── API Gateway
│
├── config-server/
│   └── Centralized configuration
│
├── frontend/
│   └── React application
│
└── README.md
```

---

## ⚙️ Getting Started

### Prerequisites

Make sure the following are installed:

* Java 17+
* Maven
* Node.js
* npm
* PostgreSQL or MySQL
* RabbitMQ
* Keycloak
* Git

---

## 🔧 Configuration

Before running the application, configure:

### Database

Configure your database credentials in the appropriate service configuration.

```properties
spring.datasource.url=YOUR_DATABASE_URL
spring.datasource.username=YOUR_USERNAME
spring.datasource.password=YOUR_PASSWORD
```

### Google Gemini API

Add your Gemini API key to the AI service configuration.

```properties
GEMINI_API_KEY=YOUR_API_KEY
```

> ⚠️ Never commit API keys, passwords, or other secrets to GitHub.

### RabbitMQ

Configure your RabbitMQ connection:

```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=YOUR_USERNAME
spring.rabbitmq.password=YOUR_PASSWORD
```

### Keycloak

Configure your Keycloak server, realm, client, and authentication settings.

---

## ▶️ Running the Application

Start the infrastructure services first.

### 1. Start RabbitMQ

Make sure RabbitMQ is running.

### 2. Start Keycloak

Start your Keycloak server and configure the required realm and client.

### 3. Start Config Server

```bash
cd config-server
mvn spring-boot:run
```

### 4. Start Eureka Server

```bash
cd eureka-server
mvn spring-boot:run
```

### 5. Start Microservices

Start:

```text
User Service
Activity Service
AI Service
```

### 6. Start API Gateway

```bash
cd api-gateway
mvn spring-boot:run
```

### 7. Start React Frontend

```bash
cd frontend
npm install
npm start
```

---

## 🔐 Authentication Flow

FitNova uses **Keycloak + OAuth 2.0 PKCE** for secure authentication.

```text
User
 ↓
React Frontend
 ↓
Keycloak
 ↓
Authentication
 ↓
Authorization Code
 ↓
PKCE Token Exchange
 ↓
Access Token
 ↓
API Gateway
 ↓
Protected Microservices
```

---

## 🐇 Asynchronous Communication

RabbitMQ is used to decouple activity processing from AI processing.

When a user submits an activity:

```text
Frontend
   ↓
Activity Service
   ↓
Save Activity
   ↓
Publish Message
   ↓
RabbitMQ
   ↓
AI Service
   ↓
Gemini API
   ↓
Generate Recommendation
```

This improves scalability and prevents AI processing from slowing down the activity API.

---

##
