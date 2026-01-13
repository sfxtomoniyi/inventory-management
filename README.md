
# Simple Inventory Management API

A RESTful API built with NestJS and SQLite to manage a small inventory of products for a fictional shop. This project was developed as part of the NextGen Interns Phase 2 task.

---

## Table of Contents

- [Description](#description)
- [Tech Stack](#tech-stack)
- [Setup Instructions](#setup-instructions)
- [API Endpoints](#api-endpoints)
- [Assumptions Made](#assumptions-made)
- [Trade-offs & Decisions](#trade-offs--decisions)
- [Next Steps / Optional Enhancements](#next-steps--optional-enhancements)

---

## Description

This project demonstrates a clean, modular REST API with proper separation of concerns. It focuses on:

- Modular NestJS structure (Controller ≠ Service ≠ Repository)
- Database integration with SQLite
- Input validation using DTOs and `class-validator`
- Proper error handling with NestJS exceptions
- Clear, maintainable code structure

The API allows managing a simple inventory with full CRUD operations on products.

---

## Tech Stack

- **Node.js LTS**
- **NestJS** (Framework)
- **TypeORM** (ORM for database interactions)
- **SQLite** (Lightweight file-based database)
- **class-validator / class-transformer** (Input validation)

---

## Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd <repository-folder>
````

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Run the application**

   ```bash
   npm run start:dev
   ```

   The server will start on `http://localhost:3000`.

4. **Test the API endpoints** using Postman, Insomnia, or `curl`.

**Note:**
The SQLite database file (`inventory.sqlite`) is automatically created when the application starts.
`synchronize: true` is enabled for development, so the schema is generated automatically. In production, migrations should be used instead.

---

## API Endpoints

| Method | Endpoint        | Description          | Notes                                                    |
| ------ | --------------- | -------------------- | -------------------------------------------------------- |
| POST   | `/products`     | Create a new product | Validates input; name ≥ 3 chars, price > 0, quantity ≥ 0 |
| GET    | `/products`     | List all products    | Optional query: `minPrice`, `maxPrice`, `inStock`        |
| GET    | `/products/:id` | Get a product by ID  | Returns 404 if not found                                 |
| PUT    | `/products/:id` | Update a product     | Partial updates allowed; updates `updatedAt`             |
| DELETE | `/products/:id` | Delete a product     | Returns 404 if the product does not exist                |

---

## Assumptions Made

* Product names are at least 3 characters long.
* Price must be greater than 0; quantity must be ≥ 0.
* Partial updates are allowed on `PUT /products/:id`.
* Query parameters on `GET /products` are optional.
* Database is file-based and does not require migrations for development.

---

## Trade-offs & Decisions

* `synchronize: true` was used to automatically create the database schema.
  In production, migrations should be used to manage schema changes safely.
* SQLite was chosen for simplicity and portability in a small-scale inventory project.
* DTOs and validation decorators (`class-validator`) ensure data integrity.
* Controllers delegate all business logic to services to maintain a clean modular structure.
* Bonus features like pagination, low-stock endpoints, and seeding were not implemented in this version.

---

## Next Steps / Optional Enhancements

* Implement pagination for `GET /products` with `page` and `limit` query parameters.
* Add a `/products/low-stock` endpoint to quickly identify products with low inventory.
* Seed the database with sample products for easier testing.
* Write unit tests for the service layer to ensure reliability.
* Switch from `synchronize: true` to proper TypeORM migrations for production-readiness.

---

## Notes

This project demonstrates best practices in NestJS development for a small inventory system:

* Separation of concerns (Controller ≠ Service ≠ Repository)
* Validation and error handling using NestJS exceptions
* Clear project structure and modular code
* Lightweight, portable database setup

```
