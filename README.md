# Carsties

Carsties is a microservices-based auction platform built with **.NET 8**, **Next.js**, and modern cloud-native technologies.  
This repository follows along with the [Udemy course](https://www.udemy.com/course/build-a-microservices-app-with-dotnet-and-nextjs-from-scratch/) by TryCatchLearn and expands it with real-world tooling and patterns.

---

## 🚀 Tech Stack

- **Backend Services**: ASP.NET Core Web API, gRPC
- **Frontend**: Next.js (React, Tailwind, Flowbite, Zustand, NextAuth.js)
- **Messaging**: RabbitMQ with MassTransit
- **Databases**: PostgreSQL, MongoDB
- **Authentication**: Duende IdentityServer with ASP.NET Identity
- **API Gateway**: YARP (reverse proxy)
- **Realtime**: SignalR (notifications)
- **Containerization**: Docker & Docker Compose
- **Testing**: xUnit, Moq
- **CI/CD**: GitHub + Git CLI

---

## 🏗️ Project Setup

### Clone the Repository
```bash
git clone https://github.com/brunsdon/Carsties.git
cd Carsties
```

### .NET Environment
```bash
dotnet --info
dotnet new sln
dotnet new globaljson --sdk-version 8.0.413
```

---

## 📦 Services Overview

### Auction Service
- ASP.NET Core Web API
- Entity Framework Core migrations
- Exposes REST API at: `http://localhost:7001/api/auctions`

```bash
dotnet new webapi -o src/AuctionService
dotnet sln add src/AuctionService
dotnet ef migrations add "InitialCreate" -o Data/Migrations
dotnet ef database update
```

### Search Service
- ASP.NET Core Web API
- MongoDB for persistence

```bash
dotnet new webapi -o src/SearchService -controllers
dotnet sln add src/SearchService
```

### Contracts
- Shared library for event messages
```bash
dotnet new classlib -o src/Contracts
dotnet sln add src/Contracts
```

### Identity Service
- Duende IdentityServer + ASP.NET Identity
- PostgreSQL for user storage

Default Users:
- **alice / Pass123$**
- **bob / Pass123$**

```bash
dotnet new duende-is-aspid -o src/IdentityService
dotnet sln add src/IdentityService
```

### Gateway Service
- Reverse proxy with **YARP**
- Central entry point for client requests
- Handles SSL termination, URL rewriting, and load balancing

### Bidding Service
- gRPC + ASP.NET Core
- Uses Kestrel with HTTP/2

### Notification Service
- SignalR for real-time auction updates

---

## 🌐 Frontend (Next.js)

Setup:
```bash
npx create-next-app@latest web-app
cd web-app
npm install
npm run dev
```

Libraries:
- **Flowbite React** (UI components)
- **Zustand** (state management)
- **NextAuth.js (Auth.js)** for authentication with Duende
- **React Hook Form**, **React Datepicker**
- **SignalR client** for notifications
- **React Hot Toast** for UX feedback
- **Date-fns** for formatting
- **Axios / SWR** for data fetching

---

## 🐳 Docker

Build & Run:
```bash
docker compose build
docker compose up -d
docker compose down -v
```

Check volumes:
```bash
docker volume list
docker volume rm [volume name]
```

Healthchecks:
- [docker-compose-healthchecks](https://github.com/peter-evans/docker-compose-healthcheck)

---

## 🧪 Testing

Unit Tests with **xUnit** + **Moq**:
```bash
dotnet new xunit -o tests/AuctionService.UnitTests
dotnet sln add tests/AuctionService.UnitTests
dotnet add reference ../../src/AuctionService
```

Naming convention:
```
Method_Scenario_ExpectedResult
```

---

## 🔗 Resources

- [Udemy Course](https://www.udemy.com/course/build-a-microservices-app-with-dotnet-and-nextjs-from-scratch/)  
- [Carsties Sample Repo (TryCatchLearn)](https://github.com/TryCatchLearn/Carsties)  
- [Duende IdentityServer](https://duendesoftware.com/products/identityserver)  
- [MassTransit](https://masstransit.io)  
- [YARP](https://microsoft.github.io/reverse-proxy/)  
- [Next.js](https://nextjs.org/)  
- [Flowbite React](https://flowbite-react.com/)  

---

## 📝 Git Workflow

```bash
git add .
git commit -m "End of section X"
git push origin main
```

Initialize repo:
```bash
git init
git remote add origin https://github.com/brunsdon/Carsties.git
git push -u origin main
```

---

## 📌 Notes

- RabbitMQ: `localhost:15672` (u: guest / p: guest)  
- JWT inspection: [jwt.io](https://jwt.io)  
- Default DB credentials for local dev are in docker-compose files.  
