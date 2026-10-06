<div align="center">

# FastAPI for Machine Learning

**A hands-on, module-by-module path from your first FastAPI endpoint to tested, cached, and monitored ML model APIs.**

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-v2-E92063?logo=pydantic&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?logo=sqlalchemy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)
![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?logo=pytest&logoColor=white)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [Modules](#modules)
  - [1. Introduction to FastAPI](#1-introduction-to-fastapi)
  - [2. Building APIs](#2-building-apis)
  - [3. Database Integration Project](#3-database-integration-project)
  - [4. Machine Learning Integration](#4-machine-learning-integration)
  - [5. Advanced FastAPI Concepts](#5-advanced-fastapi-concepts)
  - [6. Testing & Debugging](#6-testing--debugging)
  - [7. Performance Optimization and Monitoring](#7-performance-optimization-and-monitoring)
- [Getting Started](#getting-started)
- [Running the Examples](#running-the-examples)
- [Tech Stack](#tech-stack)
- [Notes](#notes)

---

## Overview

This repository contains my work through a structured course on building production-style APIs for machine learning with **FastAPI**. Each numbered folder is a self-contained module that builds on the previous one:

| # | Module | Key Topics |
|---|--------|-----------|
| 1 | Introduction to FastAPI | First app, type hints |
| 2 | Building APIs | CRUD, Pydantic models & validation, sync vs. async |
| 3 | Database Integration | SQLAlchemy ORM, SQLite, dependency-injected sessions |
| 4 | Machine Learning Integration | Model training, serialization (pickle / joblib / Keras), prediction endpoints |
| 5 | Advanced FastAPI Concepts | Dependency injection, API keys, OAuth2 + JWT, middleware |
| 6 | Testing & Debugging | Unit, integration, and end-to-end tests, mocking ML models, logging, exception handling |
| 7 | Performance & Monitoring | Redis caching, profiling, load testing with Locust, Prometheus + Grafana with Docker |

---

## Repository Structure

```text
Fast-API-for-Machine-Learning/
├── 1. Introduction to Fast API/
│   ├── main.py                      # Hello-world FastAPI app
│   └── practice.py                  # Python type-hint basics
│
├── 2. Building APIs/
│   ├── basic-app.py                 # Minimal app
│   ├── main.py                      # Employee CRUD API (in-memory)
│   ├── models.py / models_val.py    # Pydantic models, with Field validation
│   ├── pydantic-demo.py             # response_model usage
│   ├── sync-demo.py / async-demo.py # Blocking vs. concurrent execution
│   └── async_main.py                # Async endpoint
│
├── 3. Database Integration Project/
│   └── crud-app/
│       ├── database.py              # Engine, SessionLocal, Base
│       ├── models.py                # SQLAlchemy ORM model
│       ├── schemas.py               # Pydantic request/response schemas
│       ├── crud.py                  # DB operations
│       ├── main.py                  # REST endpoints
│       └── sqlite-demo.py           # Inspect the SQLite DB directly
│
├── 4. Machine Learning Integration/
│   ├── pickle_joblib_serialization.ipynb
│   ├── keras-serialization.ipynb
│   └── ML-Model/
│       ├── train.py                 # Train & save a housing price model
│       ├── predict.py               # Single & batch inference
│       ├── schemas.py               # Validated input/output schemas
│       └── main.py                  # Prediction API
│
├── 5. Advanced FastAPI Concepts/
│   ├── api-keys/                    # Header-based & .env-based API keys
│   ├── dependency-injection/        # Config, DB connection, user auth
│   ├── jwt-authentication/          # OAuth2 password flow + JWT + bcrypt
│   └── middleware/                  # CORS, GZip, HTTPS redirect, custom timer
│
├── 6. Testing & Debugging/
│   ├── unit-testing/                # pytest on pure business logic
│   ├── integration-testing/         # TestClient against API + logic
│   ├── e2e-testing/                 # Full request/response flow
│   ├── mock-ml/                     # Iris classifier with mocked model in tests
│   └── debugging-techniques/        # Logging & global exception handling
│
└── 7. Performance Optimization and Monitoring/
    ├── redis-setup.py               # Redis connectivity check
    ├── prometheus-setup.py          # Metrics instrumentation
    ├── caching/
    │   ├── db-caching/              # Cache SQLite query results in Redis
    │   ├── external-api-caching/    # Cache third-party API responses
    │   └── ml-caching/              # Cache model predictions
    ├── profiling/                   # Timing middleware, cProfile, line_profiler
    ├── locust-demo/                 # Load testing
    ├── demo1/                       # FastAPI + Prometheus (Docker Compose)
    └── demo2/                       # FastAPI + Prometheus + Grafana (Docker Compose)
```

---

## Modules

### 1. Introduction to FastAPI

📁 [`1. Introduction to Fast API`](1.%20Introduction%20to%20Fast%20API)

- `main.py` is a minimal FastAPI application with a single `GET /` route.
- `practice.py` shows how Python type hints work, and that they are not enforced at runtime. This is the gap Pydantic fills later.

### 2. Building APIs

📁 [`2. Building APIs`](2.%20Building%20APIs)

- **Employee management CRUD API** (`main.py`) backed by an in-memory list, with proper `HTTPException` handling (`400` duplicate, `404` not found).

  | Method | Endpoint | Description |
  |--------|----------|-------------|
  | `GET` | `/employees` | List all employees |
  | `GET` | `/employee/{emp_id}` | Get one employee |
  | `POST` | `/employees` | Add an employee |
  | `PUT` | `/update_employee/{emp_id}` | Update an employee |
  | `DELETE` | `/delete_employee/{emp_id}` | Delete an employee |

- **Data validation** with Pydantic `Field` constraints (`gt`, `min_length`, `max_length`, `ge`) and `StrictInt` (`models_val.py`).
- **Response models** that shape and validate output (`pydantic-demo.py`).
- **Sync vs. async**: `sync-demo.py` runs tasks back-to-back (~6 s), while `async-demo.py` runs them concurrently with `asyncio.gather` (~3 s).

### 3. Database Integration Project

📁 [`3. Database Integration Project/crud-app`](3.%20Database%20Integration%20Project/crud-app)

A persistent employee CRUD service built with **SQLAlchemy** and **SQLite**, organised into separate layers:

- `database.py` holds the engine and session factory.
- `models.py` defines the ORM table.
- `schemas.py` holds the Pydantic schemas (`EmployeeCreate`, `EmployeeUpdate`, `EmployeeOut`) with `EmailStr` validation.
- `crud.py` contains the data access functions.
- `main.py` defines the routes, with a `get_db()` dependency that opens and closes a session per request.

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/employees` | Create employee |
| `GET` | `/employees` | List employees |
| `GET` | `/employees/{emp_id}` | Get employee |
| `PUT` | `/employees/{emp_id}` | Update employee |
| `DELETE` | `/employees/{emp_id}` | Delete employee |

### 4. Machine Learning Integration

📁 [`4. Machine Learning Integration`](4.%20Machine%20Learning%20Integration)

- **Model serialization notebooks** compare `pickle`, `joblib`, and the native Keras `.keras` format.
- **Housing price prediction API** ([`ML-Model/`](4.%20Machine%20Learning%20Integration/ML-Model)):
  - `train.py` trains a `LinearRegression` model on the California Housing dataset and saves it as `model.joblib`.
  - `predict.py` loads the model once at startup and exposes single and vectorised batch inference.
  - `schemas.py` validates inputs (positive values, strict integers for room counts).

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Welcome message |
| `POST` | `/prediction` | Predict price for one house |
| `POST` | `/batch_prediction` | Predict prices for a list of houses |

<details>
<summary>Example request</summary>

```bash
curl -X POST http://127.0.0.1:8000/prediction \
  -H "Content-Type: application/json" \
  -d '{
        "longitude": -122.23,
        "latitude": 37.88,
        "housing_median_age": 41,
        "total_rooms": 880,
        "total_bedrooms": 129,
        "population": 322,
        "households": 126,
        "median_income": 8.3252
      }'
```

Response shape:

```json
{ "predicted_price": <float> }
```

</details>

### 5. Advanced FastAPI Concepts

📁 [`5. Advanced FastAPI Concepts`](5.%20Advanced%20FastAPI%20Concepts)

| Topic | Files | What it shows |
|-------|-------|---------------|
| **Dependency Injection** | `dependency-injection/` | Injecting settings, yield-based DB connection lifecycle, and current-user resolution with `OAuth2PasswordBearer` |
| **API Keys** | `api-keys/` | Validating an `api-key` header, with the key hard-coded or loaded from `.env` via `pydantic-settings` |
| **JWT Authentication** | `jwt-authentication/` | OAuth2 password flow, bcrypt password hashing (`passlib`), JWT creation/verification with expiry (`authlib`) |
| **Middleware** | `middleware/` | `CORSMiddleware`, `GZipMiddleware`, `HTTPSRedirectMiddleware`, and a custom request-timing middleware |

### 6. Testing & Debugging

📁 [`6. Testing & Debugging`](6.%20Testing%20%26%20Debugging)

Built around a **loan eligibility** service (income ≥ 50,000, age ≥ 21, employed):

| Level | Folder | Approach |
|-------|--------|----------|
| Unit | `unit-testing/` | `pytest` on the pure `is_eligible_for_loan` function, including boundary cases |
| Integration | `integration-testing/` | `TestClient` exercising the endpoint together with the logic module |
| End-to-End | `e2e-testing/` | Full HTTP request/response checks for pass and fail scenarios |
| ML Mocking | `mock-ml/` | Iris classifier endpoint tested with `unittest.mock.patch` so tests don't depend on the real model |

**Debugging techniques** (`debugging-techniques/`) cover structured logging configuration and a global `@app.exception_handler` that returns clean JSON errors.

### 7. Performance Optimization and Monitoring

📁 [`7. Performance Optimization and Monitoring`](7.%20Performance%20Optimization%20and%20Monitoring)

- **Caching with Redis**, using SHA-256 cache keys and TTL expiry:
  - `db-caching/` caches SQLite query results.
  - `external-api-caching/` caches responses from an external API (JSONPlaceholder) fetched with async `httpx`.
  - `ml-caching/` caches model predictions keyed on the input features.
- **Profiling**:
  - `time-demo.py` adds a request-timing middleware with logging.
  - `cprofile-demo.py` saves a `.prof` file per request.
  - `line-profiler-demo/` profiles line by line with `kernprof`.
- **Load testing**: `locust-demo/` simulates concurrent users against API endpoints.
- **Monitoring**:
  - `prometheus-setup.py` exposes `/metrics` with `prometheus-fastapi-instrumentator`.
  - `demo1/` runs FastAPI and Prometheus with Docker Compose.
  - `demo2/` runs FastAPI, Prometheus, and Grafana with Docker Compose.

---

## Getting Started

### Prerequisites

- Python **3.10+**
- [Docker](https://www.docker.com/) & Docker Compose (for Module 7 monitoring demos)
- [Redis](https://redis.io/) running on `localhost:6379` (for Module 7 caching demos)

### Installation

```bash
# Clone the repository
git clone https://github.com/SohamSadakal31/Fast-API-for-Machine-Learning.git
cd Fast-API-for-Machine-Learning

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# Install dependencies
pip install fastapi uvicorn pydantic pydantic-settings "pydantic[email]" \
            sqlalchemy scikit-learn pandas numpy joblib \
            "passlib[bcrypt]" authlib python-multipart \
            pytest httpx redis locust line_profiler \
            prometheus-fastapi-instrumentator
```

> For the Keras serialization notebook, also install `tensorflow` and `jupyter`.

---

## Running the Examples

Most examples are standalone FastAPI apps. Run them from **inside their own folder** so that relative imports and model files (`model.joblib`, `test.db`) resolve correctly.

```bash
# Start an app
cd "4. Machine Learning Integration/ML-Model"
uvicorn main:app --reload
```

Then open the interactive docs:

- Swagger UI: http://127.0.0.1:8000/docs
- ReDoc: http://127.0.0.1:8000/redoc

Single-file demos run the same way, using the file name as the module, e.g. `uvicorn custom-middleware:app --reload`.

### Run the tests

```bash
cd "6. Testing & Debugging/unit-testing"        && pytest -v
cd "../integration-testing"                     && pytest -v
cd "../e2e-testing"                             && pytest -v
cd "../mock-ml"                                 && pytest -v
```

### Load testing with Locust

```bash
cd "7. Performance Optimization and Monitoring/locust-demo"
uvicorn main:app --port 8000          # terminal 1
locust -f locustfile.py --host http://127.0.0.1:8000   # terminal 2 → open http://localhost:8089
```

### Line profiling

```bash
cd "7. Performance Optimization and Monitoring/profiling/line-profiler-demo"
kernprof -l -v profiling_test.py
```

### Monitoring stack (Prometheus + Grafana)

```bash
cd "7. Performance Optimization and Monitoring/demo2"
docker compose up --build
```

| Service | URL |
|---------|-----|
| FastAPI | http://localhost:8000 |
| Metrics | http://localhost:8000/metrics |
| Prometheus | http://localhost:9090 |
| Grafana | http://localhost:3000 (default login `admin` / `admin`) |

In Grafana, add Prometheus as a data source using `http://prometheus:9090`.

---

## Tech Stack

| Category | Tools |
|----------|-------|
| Framework | FastAPI, Uvicorn, Starlette |
| Validation | Pydantic, pydantic-settings |
| Database | SQLAlchemy, SQLite |
| Machine Learning | scikit-learn, NumPy, pandas, joblib, Keras |
| Security | OAuth2, JWT (Authlib), Passlib (bcrypt), API keys |
| Testing | pytest, FastAPI `TestClient`, `unittest.mock` |
| Performance | Redis, httpx, cProfile, line_profiler, Locust |
| Monitoring & DevOps | Prometheus, Grafana, Docker, Docker Compose |

---

## Notes

- Credentials and secret keys in the authentication examples (`my_secret`, `secret123`, etc.) are **for demonstration only**. In real deployments, load secrets from environment variables or a secrets manager.
- `.env` files, virtual environments, profiling output, and cache artifacts are excluded via `.gitignore`.

---

<div align="center">

**Author:** [Soham Sadakal](https://github.com/SohamSadakal31)

If you find this repository useful, consider giving it a ⭐

</div>
