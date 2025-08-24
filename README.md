# Hahn Software – .NET 9 + React Assignment

This repository implements a small but realistic application demonstrating **Clean Architecture**, **CQRS with MediatR**, **DDD-flavored domain events**, **EF Core**, **Swagger**, **Docker Compose**, and **TypeScript (React)**.

## Tech Stack
- .NET 9 (API)
- Clean Architecture (Domain / Application / Infrastructure / API)
- CQRS via **MediatR**
- EF Core (SQL Server)
- FluentValidation
- Swagger / OpenAPI
- React + TypeScript (Vite)
- Docker Compose (API + SQL Server)
- xUnit tests

## Prerequisites
- .NET SDK 9.x
- Node.js 18+
- Docker Desktop
- (Optional) PowerShell for scripts

## Getting Started (Local Dev)

```bash
# Restore & build
dotnet restore
dotnet build

# (First time) create EF Core migration & update DB
dotnet tool update --global dotnet-ef
dotnet ef migrations add InitialCreate --project src/Infrastructure --startup-project src/API --output-dir Persistence/Migrations
dotnet ef database update --project src/Infrastructure --startup-project src/API

# Run API
dotnet run --project src/API
# Swagger: http://localhost:5000/swagger
```

In another terminal:
```bash
# Frontend
cd frontend/react-app
npm install
npm run dev
# If needed, set VITE_API in .env to http://localhost:5000
```

## Docker
```bash
docker compose up --build
# API will be exposed (e.g., http://localhost:5000)
```

## Tests
```bash
dotnet test
```

## Notes
- **MediatR** is used to wire Commands/Queries and to publish **domain events** via an EF Core **SaveChanges interceptor**.
- CORS is enabled in Development for `http://localhost:5173` and `http://localhost:3000`.
- Please see `src/Infrastructure/Persistence/DomainEventsInterceptor.cs` for event dispatching.
