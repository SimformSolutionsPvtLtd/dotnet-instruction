# GitHub Copilot Custom Instructions – .NET Best Practices

This file defines the coding standards, architectural principles, and best practices that GitHub Copilot must follow when generating or suggesting code for this repository.

---

## General Guidelines
- Follow **SOLID principles** and **Clean Code** practices.
- Ensure all code is **readable, maintainable, and self-documenting**.
- Use meaningful names: **PascalCase** for classes, methods, properties; **camelCase** for variables and parameters; **UPPER_CASE** for constants.
- Avoid **hardcoding values** – always use configuration files (`appsettings.json`, environment variables, or secrets managers).
- Use **async/await** for all I/O-bound operations.
- Maintain consistent **indentation (4 spaces)** for all files.
- Always add **XML documentation comments** (`///`) for:
  - Public classes
  - Public methods and properties
  - Interfaces
  - API endpoints

---

## Architecture & Design
- Adopt **Clean Architecture (Repository Architecture)**:
  - Separate concerns between API, application services, domain, and infrastructure.
  - No business logic in controllers.
- Enforce **Dependency Injection (DI)** for all services.
- Use **Interfaces** for abstractions and to support unit testing.
- Avoid **tight coupling** and **cyclic dependencies**.
- For complex workflows, consider **CQRS + MediatR**.

---

## API Best Practices
- Follow **RESTful standards**:
  - Use correct HTTP verbs (`GET`, `POST`, `PUT`, `DELETE`).
  - Return proper status codes and standard response structures.
- Version APIs (`/api/v1/...`).
- Implement **global exception handling middleware**.
- Return **ProblemDetails** (RFC 7807) or consistent response wrappers.
- Enable **Swagger/OpenAPI** for documentation.
- Apply **jwt authentication** and proper authorization policies.

---

## Error Handling & Logging
- Use **try-catch** only where necessary.
- Avoid silent catches (`catch { }`).
- Log exceptions with **structured logging** (`ILogger<T>`/Serilog).
- Do not expose **internal exception details** to users.

---

## Performance Best Practices
- Use asynchronous database operations (`SaveChangesAsync()`, `ToListAsync()`).
- Avoid unnecessary LINQ inside loops.
- Use **`AsNoTracking()`** for read-only queries.
- Cache frequently used data (MemoryCache, Redis).
- Use **IAsyncEnumerable<T>** for streaming large datasets.
- Avoid excessive allocation and dispose resources with `using`/`await using`.

---

## Security Best Practices
- Use **parameterized queries** or ORM (Entity Framework) to prevent SQL Injection.
- Store sensitive data in **Azure Key Vault / AWS Secrets Manager**.
- Always validate inputs (FluentValidation/Data Annotations).
- Do not log passwords, tokens, or PII.
- Use HTTPS, JWT/OAuth2, or Azure AD for authentication.

---

## Entity Framework Guidelines
- Prefer **code-first with migrations**.
- Avoid multiple `SaveChanges` in a single transaction.
- Disable **lazy loading** in critical performance areas.
- Use **DbContext pooling** in high-load applications.

---

## Testing Practices
- Write **unit tests** for business logic (xUnit/NUnit/MSTest).
- Use **Moq/FakeItEasy/NSubstitute** for mocking.
- Follow **Arrange-Act-Assert (AAA)** pattern.
- Write **integration tests** for APIs and database flows.
- Ensure tests are **independent and repeatable**.

---

## Code Quality
- Enable **nullable reference types** (`#nullable enable`).
- Follow Microsoft .NET **Code Analysis rules (CAxxxx)**.
- Dispose resources properly.
- Avoid **static classes with mutable state**.
- Use **record types** for immutable models.
- Maintain **consistent indentation (4 spaces)** across all code files.
- Add **XML documentation comments** (`///`) for all public members.

---

## Deployment & DevOps
- Keep environment-specific configs in `appsettings.{Environment}.json`.
- Use **CI/CD pipelines** for build, test, and deploy.
- Implement **health checks** (`/health`) for monitoring.
- Automate database migrations during deployment.

---

### Instructions for Copilot
When generating or suggesting code:
1. Always adhere to these best practices.
2. Prefer **async programming** for I/O-bound operations.
3. Suggest **dependency-injected services** over static helpers.
4. Recommend **secure, scalable patterns**.
5. Follow **clean architecture layering** (API → Application → Domain → Infrastructure).
6. Add **XML documentation comments for all public members**.
7. Maintain **4-space indentation and consistent code formatting**.

