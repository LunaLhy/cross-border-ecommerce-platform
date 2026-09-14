# Cross-Border E-Commerce Platform

A full-stack e-commerce portfolio project for managing products, customer orders, inventory, and supplier imports. The platform is designed to grow into a cross-border workflow where supplier costs in CNY can be converted to VND before products are sold locally.

## Project goals

- Build a production-style REST API with Java and Spring Boot.
- Build a responsive customer and administrator interface with React.
- Apply secure authentication and role-based authorization.
- Model realistic e-commerce processes: products, carts, orders, stock, and order status.
- Add cross-border supplier and import-order capabilities after the core store is stable.

## MVP scope

The first release deliberately focuses on the essential shopping flow:

- Browse, search, filter, and view products.
- Register and sign in with JWT authentication.
- Add products to a cart and change quantities.
- Place orders and view order history.
- Allow administrators to manage categories, products, inventory, and orders.

The following are planned after the MVP: real payment integration, CNY/VND exchange rates, supplier management, import orders, Redis caching, RabbitMQ messaging, MongoDB, and CI/CD.

## Technology stack

| Area | Technology |
| --- | --- |
| Frontend | React, JavaScript, HTML5, CSS3, React Router, Axios, Tailwind CSS |
| Backend | Java, Spring Boot, Spring MVC, Spring Security, Spring Data JPA, Hibernate, Maven |
| Database | PostgreSQL |
| API tools | REST API, JSON, Postman, Swagger / OpenAPI |
| Development tools | Git, GitHub, Docker, Docker Compose, Linux |
| Future services | Redis, RabbitMQ, Nginx, MongoDB |

## High-level architecture

```text
React frontend
     |
     | HTTPS / JSON REST API
     v
Spring Boot backend
     |
     +-- Spring Security + JWT
     +-- Product / Cart / Order / Admin modules
     |
     v
PostgreSQL

Future: Redis cache, RabbitMQ events, MongoDB documents, Nginx reverse proxy
```

## Core roles

| Role | Permissions |
| --- | --- |
| Guest | Browse products and search the catalogue |
| User | Manage profile and cart, place orders, view order history |
| Admin | Manage products, categories, stock, users, and order status |

## Order lifecycle

```text
PENDING -> CONFIRMED -> SHIPPING -> DELIVERED
                \-> CANCELLED
```

> The backend is the source of truth for product price, inventory, order total, and order-state transitions. Never trust these values when they come directly from the frontend.

## Initial database model

```text
users
roles
user_roles
categories
products
product_images
carts
cart_items
orders
order_items
```

Future cross-border entities:

```text
suppliers
supplier_products
import_orders
exchange_rates
```

## Planned API modules

| Module | Example endpoints |
| --- | --- |
| Authentication | `POST /api/auth/register`, `POST /api/auth/login` |
| Products | `GET /api/products`, `GET /api/products/{id}` |
| Categories | `GET /api/categories` |
| Cart | `GET /api/cart`, `POST /api/cart/items` |
| Orders | `POST /api/orders`, `GET /api/orders/me` |
| Admin | `POST /api/admin/products`, `PATCH /api/admin/orders/{id}/status` |

## Repository structure

```text
cross-border-ecommerce/
├── frontend/                 # React application
├── backend/                  # Spring Boot application
├── docs/                     # Architecture, API, and database notes
├── docker-compose.yml        # Local multi-service environment (planned)
├── .gitignore
└── README.md
```

## Development roadmap

1. Create the static React pages: Home, Products, Product Detail, Cart, Login, and Admin.
2. Design the PostgreSQL schema and create the Spring Boot project.
3. Implement category and product CRUD APIs, including validation and pagination.
4. Implement user registration, login, JWT, and role-based access control.
5. Implement cart, stock validation, order creation, and order history.
6. Connect the React application to the API.
7. Build the administrator product and order-management screens.
8. Add tests, Swagger documentation, Docker Compose, and deployment documentation.
9. Extend the project with suppliers, CNY/VND conversion, and import orders.

## Getting started

The application folders will be added progressively during development.

### Prerequisites

- Git
- Java LTS and Maven
- Node.js and npm
- PostgreSQL
- Docker Desktop (recommended)
- Postman or another API client

### First setup steps

```bash
git clone <your-repository-url>
cd cross-border-ecommerce
```

When the frontend and backend are created, their individual setup commands will be documented here.

## Git workflow

Use small, focused commits:

```text
feat(product): add product search endpoint
fix(cart): prevent quantity above available stock
docs(readme): add order lifecycle
```

Avoid committing local credentials, database files, build artifacts, or environment files containing secrets.

## Definition of done for a feature

A feature is complete only when it:

- Meets its acceptance criteria.
- Handles validation and meaningful error responses.
- Has been checked through the UI or Postman.
- Does not expose unauthorized data or operations.
- Is committed with a clear message.
- Has relevant documentation updated.

## License

This project is intended for learning and portfolio purposes. Choose a license before publishing it publicly.
