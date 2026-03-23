# FastAPI

FastAPI is a modern, high-performance **Python web framework** designed for building **RESTful APIs** quickly and efficiently. Created by **Sebastián Ramírez** in **2018**, it is built on standard **Python type hints** and delivers performance comparable to **Node.js** and **Go**.

**Core Components**
FastAPI achieves its performance and reliability by leveraging three main technologies:

- **Starlette:** A lightweight ASGI framework that provides powerful async capabilities for handling concurrent requests.
- **Pydantic:** A data validation library that uses type annotations to validate, serialize, and deserialize data.
- **Uvicorn:** A lightning-fast ASGI server used to serve FastAPI applications.

**Key Features**

- **Automatic documentation:** Generates interactive API docs via **Swagger UI** (`/docs`) and **ReDoc** (`/redoc`) using the OpenAPI standard.
- **Built-in data validation:** Pydantic models validate requests and return clear errors (commonly **422 Unprocessable Entity**).
- **Asynchronous support:** Native `async`/`await` support for I/O-bound tasks like DB calls and external APIs.
- **Dependency injection:** Built-in DI for reusable components such as DB sessions or security logic.
- **Security:** Integrated support for **OAuth2**, **JWT**, **HTTP Basic**, and **API Keys**.

**Why Choose FastAPI**
FastAPI is often preferred over older frameworks like Flask or Django for API-first development because it:

- Requires less boilerplate.
- Reduces human-induced errors.
- Speeds up feature development.

---

## Routing and Request Handling

FastAPI routing maps URLs to Python functions using **path operation decorators**, while request handling uses type hints for automatic parsing, validation, and serialization.

### Routing in FastAPI

- **Path operation decorators:** Define routes with `@app.get()`, `@app.post()`, `@app.put()`, `@app.delete()`, etc.
- **Path parameters:** Dynamic URL segments become typed function arguments (e.g., `item_id: int`).
- **APIRouter for modularity:** Organize routes into modules with `APIRouter` and include them using `app.include_router()`.

### Request Handling in FastAPI

- **Query parameters:** Parsed automatically from the URL based on type hints.
- **Request body:** JSON bodies are validated against Pydantic models.
- **Headers and cookies:** Declare them explicitly with `Header` and `Cookie`.
- **Dependency injection:** Dependencies are resolved automatically and injected into endpoints.

### Request Lifecycle

1. **URL parsing and method identification.**
2. **Path and query parameter extraction.**
3. **Body deserialization and validation** (raises `RequestValidationError` on failure).
4. **Function execution** with validated inputs.
5. **Response generation** and serialization (e.g., JSON).

---

## Defining Routes and HTTP Methods

API routes are defined with **path operation decorators** applied to standard Python functions. The decorator specifies both the **HTTP method** and the **URL path**.

**Core Concepts**

- **Route path:** The endpoint URL (e.g., `/items/`).
- **HTTP method:** The action on the resource.
- **Path operation function:** The function that handles the request.

**Common HTTP Methods**

- **GET:** Retrieve data.
- **POST:** Create new data.
- **PUT:** Update existing data.
- **DELETE:** Remove data.

---

## Path Parameters

Path parameters define dynamic parts of a URL and map them to function arguments.

**Key Concepts**

- **Syntax:** Use `{}` in the path string (e.g., `@app.get("/items/{item_id}")`).
- **Automatic type conversion:** Converts to annotated types (e.g., `int`, `float`, `bool`).
- **Required by default:** Always required because they are part of the URL path.
- **Editor support:** Type hints improve autocomplete and static checks.

**Advanced Features**

- **Numeric validations:** Use `Path` for constraints like min/max.
- **Enums:** Restrict to specific values with Python `Enum` types.
- **Annotated syntax:** Use `Annotated` for clearer metadata and defaults.

---

## Query Parameters

Query parameters provide optional values and filtering capabilities. They are inferred from function parameters not declared as path parameters.

**How to Use Query Parameters**

- **Declaration:** Add parameters to the function signature (e.g., `q: str | None = None`).
- **Location:** Appear after `?` in the URL (e.g., `.../items/foo?needy=sooooneedy`).
- **Type hinting:** Enables automatic conversion and validation (e.g., `limit: int`).

**Required vs. Optional**

- **Optional parameters:** Provide a default value, commonly `None` (e.g., `q: str | None = None`).
- **Required parameters:** Omit a default value for non-path params (e.g., `needy: str`).

**Advanced Usage**

- **Extra validation:** Use `Query()` for constraints and metadata.
- **Lists:** Accept lists with `list[str]` types (e.g., `items: list[str] | None = Query(None)`).
- **Pydantic models:** Group related query params into a model for reuse.

---

## Request and Response Models

FastAPI uses **Pydantic models** to define request and response shapes. This drives **validation**, **serialization**, and **automatic OpenAPI docs**.

**Request Models**

- **Automatic validation:** Invalid data returns **422 Unprocessable Entity**.
- **Documentation:** Models generate schemas used by Swagger UI.

**Response Models**

- **Data filtering:** Only fields in `response_model` are returned (e.g., hides passwords).
- **Data serialization:** Pydantic efficiently serializes objects to JSON.

---

## Status Codes and HTTP Exceptions

FastAPI uses standard **HTTP status codes** and **HTTPException** for error signaling.

**Status Code Classes**

- **1xx Informational:** Request received, continuing process.
- **2xx Success:** Request succeeded.
- **3xx Redirection:** Further action required.
- **4xx Client Error:** Invalid request or unauthorized access.
- **5xx Server Error:** Server failed to fulfill a valid request.

**Common Status Codes**

- **200 OK**
- **201 Created**
- **204 No Content**
- **400 Bad Request**
- **401 Unauthorized**
- **403 Forbidden**
- **404 Not Found**
- **422 Unprocessable Entity**
- **500 Internal Server Error**

**Using HTTPException**

- Raise `HTTPException` to return an error response with a JSON `detail` message.
- Use `fastapi.status` constants like `status.HTTP_404_NOT_FOUND`.

---

## FastAPI vs Flask vs Django

Framework choice depends on scope, performance needs, and architectural preferences.

**Django**

- **Best for:** Large, full-stack applications needing built-in ORM, admin, auth, and security.
- **Tradeoffs:** Rigid structure; overkill for small projects.

**Flask**

- **Best for:** Small apps or teams needing full architectural freedom.
- **Tradeoffs:** Manual validation, security, and scaling patterns.

**FastAPI**

- **Best for:** High-concurrency APIs, microservices, and ML model serving.
- **Tradeoffs:** Newer ecosystem; fewer third-party plugins than Django.

---

## Role of Pydantic in FastAPI

Pydantic is the core engine for **validation**, **serialization**, and **schema generation**.

**Core Responsibilities**

- **Data validation and integrity:** Ensures incoming data matches the schema.
- **Data parsing and coercion:** Converts values to the correct types (e.g., "123" to `int`).
- **Serialization:** Shapes outgoing JSON and filters fields.
- **Automatic documentation:** Generates JSON Schema for Swagger UI and ReDoc.

**Key Features Used by FastAPI**

- **BaseModel** for schemas.
- **Field** for constraints and metadata.
- **Custom validators** via `@field_validator`.
- **BaseSettings** for configuration management.

---

## Asynchronous Programming in FastAPI

Asynchronous programming uses `async`/`await` to handle many concurrent requests efficiently.

**Key Concepts**

- **async def:** Declares an asynchronous function.
- **await:** Yields control while waiting for I/O.
- **I/O-bound operations:** Ideal for async (network, disk, DB).
- **Event loop:** Manages and schedules async tasks.

**When to Use async**

- Database queries with async drivers.
- External API calls using an async client like HTTPX.
- Asynchronous file handling with `aiofiles`.

**When to Use def**

- CPU-intensive calculations.
- Blocking libraries that do not support async.

---

## Database Integration

FastAPI works with **SQL** and **NoSQL** databases using ORMs or drivers.

**SQL Databases (Recommended: SQLModel)**

- **Tools:** SQLModel, SQLAlchemy, asyncpg, pymysql.
- **Typical flow:** Install dependencies, define models, create an engine, manage sessions with DI, implement CRUD.

**NoSQL Databases (Example: MongoDB)**

- **Tools:** PyMongo, motor.
- **Typical flow:** Install driver, connect client, perform CRUD with driver methods.

**Best Practices**

- Use **async drivers** to avoid blocking the event loop.
- Manage DB sessions with **dependency injection**.
- Store credentials in **environment variables** or `BaseSettings`.
- Use a **separate test database** for automated testing.

---

## Security and Authentication

FastAPI provides utilities in `fastapi.security` for common auth patterns.

**Security Tools**

- **OAuth2:** Includes helpers for password and authorization code flows.
- **API Keys:** `APIKeyQuery`, `APIKeyHeader`, `APIKeyCookie`.
- **HTTP Basic and Digest:** `HTTPBasic`, `HTTPDigest`.
- **OpenID Connect:** `OpenIdConnect`.

**Implementation Notes**

- Use **Depends()** or **Security()** for integration with DI and docs.
- Use **passlib** for password hashing and **secrets** for safe comparisons.

**Best Practices**

- Enforce **HTTPS** in production.
- Add **custom exception handlers** to avoid data leaks.
- Keep dependencies **up to date** for security fixes.

---

## Automatic Interactive API Documentation

FastAPI generates OpenAPI docs automatically with no extra setup.

**How It Works**

- **OpenAPI schema:** Generated from type hints and Pydantic models.
- **Swagger UI:** Available at `/docs`.
- **ReDoc:** Available at `/redoc`.

**Benefits**

- **Synchronization:** Docs stay in sync with code.
- **Interactivity:** Test endpoints directly in the browser.

**Customization**

- Add app metadata like title, description, and version.
- Group endpoints with **tags**.
- Hide or move documentation routes.

---

## Organizing Code with API Routers

Break large applications into modules for clarity and scale.

**Key Concepts**

- **Modularization:** Separate concerns into modules (models, services, routes).
- **API routers:** Group related endpoints with `APIRouter`.
- **Main app:** Include routers in a central application instance.

**Benefits**

- Cleaner codebase.
- Easier maintenance and testing.
- Improved reuse and scalability.

---

## Background Tasks and WebSockets

FastAPI supports background tasks and real-time communication.

**WebSockets**

- Install with `pip install websockets`.
- Define endpoints with `@app.websocket()` and `websocket.accept()`.
- Use a connection manager to track and broadcast to clients.

**Background Tasks**

- Inject `BackgroundTasks` and schedule work with `.add_task()`.
- Use `asyncio.create_task()` for periodic background work.

---

## Testing and Deploying FastAPI

### Testing

- **Local run:** `uvicorn main:app --reload`.
- **Manual testing:** Use Swagger UI (`/docs`) or ReDoc (`/redoc`).
- **Automated testing:** Use `pytest` for integration and unit tests.

### Deployment

- **Containerize:** Build a Docker image with a `Dockerfile` and dependencies.
- **Deploy:** Push to GitHub and connect to a platform like **Cloud Run**, **Azure App Service**, or **Heroku**.
- **Run command:** Use `uvicorn main:app --host 0.0.0.0` or Gunicorn with Uvicorn workers.
- **Secrets:** Configure environment variables securely in the platform dashboard.

---

**Reference:** https://fastapi.tiangolo.com/
