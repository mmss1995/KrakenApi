# 🐙 kraken-api-starter

> A production-ready REST API boilerplate built with **KrakenJS**, showcasing enterprise-grade Node.js architecture patterns — designed as a portfolio project for Senior Backend/Fullstack roles.

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-brightgreen?logo=node.js)](https://nodejs.org/)
[![KrakenJS](https://img.shields.io/badge/KrakenJS-2.x-blue)](https://krakenjs.com/)
[![License](https://img.shields.io/badge/license-MIT-lightgrey)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

---

## Overview

**kraken-api-starter** demonstrates a scalable, maintainable REST API using [KrakenJS](https://krakenjs.com/) — the opinionated Node.js framework built on top of Express by PayPal — with a focus on real-world architecture concerns: environment-based configuration, middleware layering, route organisation, and testability.

The project implements a simple **Product Catalog API** as a realistic domain to showcase the framework's conventions without artificial complexity.

---

## Key Features

- **KrakenJS conventions** — `config/`, `controllers/`, `models/`, `lib/` structure following PayPal's production patterns
- **Environment-aware configuration** — `confit`-based config with `development`, `staging`, and `production` profiles
- **Middleware pipeline** — Security headers (`lusca`), request logging (`morgan`), body parsing, and error handling all wired via `config/middleware.json`
- **Route auto-loading** — Controllers mapped automatically via `router` configuration, no manual `app.use()` chains
- **MongoDB integration** — Mongoose models with schema validation and repository pattern
- **Input validation** — `joi` schemas decoupled from controllers
- **Centralised error handling** — Consistent JSON error responses across all endpoints
- **Testing setup** — Unit and integration tests with `mocha`, `chai`, and `supertest`
- **Docker-ready** — `Dockerfile` and `docker-compose.yml` for local development

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | KrakenJS 2.x (Express) |
| Runtime | Node.js 18 LTS |
| Database | MongoDB 6 + Mongoose |
| Validation | Joi |
| Security | Lusca (CSRF, XSS, CSP) |
| Testing | Mocha + Chai + Supertest |
| Config | Confit + nconf |
| Logging | Morgan + custom middleware |
| Container | Docker + Docker Compose |

---

## Project Structure

```
kraken-api-starter/
├── config/
│   ├── app.json              # KrakenJS application config
│   ├── middleware.json        # Middleware pipeline declaration
│   └── config.json           # Environment-aware settings (confit)
├── controllers/
│   ├── products/
│   │   └── index.js          # Route handlers for /products
│   └── index.js              # Root controller
├── models/
│   └── product.js            # Mongoose schema + model
├── lib/
│   ├── db.js                 # MongoDB connection factory
│   ├── validators/
│   │   └── product.js        # Joi validation schemas
│   └── middleware/
│       └── errorHandler.js   # Centralised error response
├── tests/
│   ├── unit/
│   │   └── models/product.spec.js
│   └── integration/
│       └── products.spec.js
├── index.js                  # Application entry point
├── Dockerfile
├── docker-compose.yml
└── package.json
```

---

## Getting Started

### Prerequisites

- Node.js 18+
- MongoDB 6+ (or Docker)
- npm 9+

### Installation

```bash
git clone https://github.com/mmss1995/kraken-api-starter.git
cd kraken-api-starter
npm install
```

### Running locally

**With Docker (recommended):**

```bash
docker-compose up
```

**Without Docker:**

```bash
# Start MongoDB locally, then:
npm run dev
```

The API will be available at `http://localhost:8000`.

---

## API Reference

### Products

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/products` | List all products (paginated) |
| `GET` | `/products/:id` | Get a single product |
| `POST` | `/products` | Create a new product |
| `PUT` | `/products/:id` | Update a product |
| `DELETE` | `/products/:id` | Delete a product |

**Example — Create a product:**

```bash
curl -X POST http://localhost:8000/products \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Wireless Headphones",
    "price": 149.99,
    "category": "electronics",
    "stock": 50
  }'
```

**Response:**

```json
{
  "id": "64f3a2b1c9e4d500123abc01",
  "name": "Wireless Headphones",
  "price": 149.99,
  "category": "electronics",
  "stock": 50,
  "createdAt": "2024-09-02T10:23:41.000Z"
}
```

---

## Configuration

KrakenJS uses `confit` for hierarchical, environment-aware configuration. Settings in `config/config.json` are overridden per environment:

```json
// config/config.json
{
  "database": {
    "url": "env:MONGO_URI",
    "poolSize": 5
  },
  "server": {
    "port": 8000,
    "host": "localhost"
  }
}
```

Set environment variables in `.env` (copy from `.env.example`):

```bash
NODE_ENV=development
MONGO_URI=mongodb://localhost:27017/kraken_starter
```

---

## Testing

```bash
# Run all tests
npm test

# Unit tests only
npm run test:unit

# Integration tests only
npm run test:integration

# With coverage
npm run test:coverage
```

---

## Why KrakenJS?

KrakenJS was developed by PayPal to enforce a consistent project structure and middleware configuration across large Node.js teams. Unlike bare Express, it provides:

- **Convention over configuration** — predictable file layout across any team size
- **Externalised middleware** — pipeline defined in JSON, not scattered `app.use()` calls
- **Environment isolation** — config layering baked in, no custom environment logic needed
- **Battle-tested at scale** — used in production at PayPal for high-traffic financial services APIs

This project demonstrates the ability to work with opinionated enterprise frameworks and understand the trade-offs between flexibility and standardisation.

---

## Author

**Matteo** — Senior Frontend Developer & Architect  
[GitHub](https://github.com/mmss1995) · [LinkedIn](https://linkedin.com/in/yourprofile)

---

## License

MIT © Matteo
