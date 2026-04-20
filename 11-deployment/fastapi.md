# FastAPI

FastAPI is a modern, high-performance **Python web framework** designed for building **RESTful APIs** quickly and efficiently. Created by **Sebastián Ramírez** in **2018**, it is built on standard **Python type hints** (a formal syntax used to indicate the expected data types of variables, function arguments, and return values) and delivers performance comparable to **Node.js** and **Go**.

FastAPI achieves its performance and reliability by leveraging three main technologies:

- **Starlette:** A lightweight ASGI framework that provides powerful async capabilities for handling concurrent requests.
- **Pydantic:** A data validation library that uses type annotations to validate, serialize, and deserialize data.
- **Uvicorn:** A lightning-fast ASGI server used to serve FastAPI applications.

Here are some key features,

- **Automatic documentation:** Generates interactive API docs via **Swagger UI** (`/docs`) and **ReDoc** (`/redoc`) using the OpenAPI standard.
- **Built-in data validation:** Pydantic models validate requests and return clear errors (commonly **422 Unprocessable Entity**).
- **Asynchronous support:** Native `async`/`await` support for I/O-bound tasks like DB calls and external APIs.
- **Dependency injection:** Built-in DI for reusable components such as DB sessions or security logic.
- **Security:** Integrated support for **OAuth2**, **JWT**, **HTTP Basic**, and **API Keys**.

**Why Choose FastAPI**
FastAPI is often preferred over older frameworks like Flask or Django for API-first development because it:

- Asynchronous Support: Its native async/await support makes it ideal for I/O-bound tasks, such as calling external AI models or handling multiple concurrent requests without blocking.
- Automatic Documentation: It automatically generates interactive Swagger UI and ReDoc pages, which is a major time-saver for testing and collaborating with frontend teams.
- Data Validation & Type Safety: By leveraging Pydantic and Python type hints, it provides robust data validation and editor autocompletion, catching bugs before runtime.
- Developer Experience (DX): The framework is easy to learn for anyone already familiar with basic Python.
- Performance: Benchmarks often show it rivaling Node.js and Go in raw speed, thanks to its foundation on Starlette and Uvicorn

---

## Routing and Request Handling

FastAPI routing maps URLs to Python functions using **path operation decorators**, while request handling uses type hints for automatic parsing, validation, and serialization.

### Routing in FastAPI

- **Path operation decorators:** Define routes with `@app.get()`, `@app.post()`, `@app.put()`, `@app.delete()`, etc.
- **Path parameters:** Dynamic URL segments become typed function arguments (e.g., item_id: int). When you declare a variable in the URL path using curly braces {} and match it to a function parameter with a type hint, FastAPI automatically converts the incoming string value to that type.
- **APIRouter for modularity:** Organize routes into modules with `APIRouter` and include them using `app.include_router()`. It used to merge routes from an APIRouter instance into the main application or another router. It is the primary tool for structuring large applications by splitting endpoints into multiple files.

### Request Handling in FastAPI

FastAPI handles requests by mapping HTTP methods and paths to Python functions, using Pydantic models for automatic data validation and OpenAPI for interactive documentation.

**Declaring Request Parameters**
FastAPI automatically identifies where to extract data based on Python type hints:

- Path Parameters: Defined in the URL string (e.g., /items/{item_id}). FastAPI validates the type and passes it to your function.
- Query Parameters: Function parameters not in the path (e.g., q: str = None). These are extracted from the URL query string.
- Request Body: Declared using Pydantic models. FastAPI reads the JSON body, validates it, and converts it to a Python object.
- Form & File Data: Handled using Form and File classes for multipart/form-data or application/x-www-form-urlencoded payloads.

**Accessing the Raw Request Object**
In advanced cases, you can access the underlying Starlette Request object directly to get client IP addresses, headers, or cookies that aren't defined as parameters:

**Concurrency and Execution**
FastAPI's performance stems from how it handles concurrent requests:

- async def: Used for I/O-bound tasks (database calls, external APIs). These run on the main event loop, allowing thousands of concurrent connections.
- def (Synchronous): Used for CPU-bound or standard blocking tasks. FastAPI runs these in a separate thread pool to avoid blocking the main event loop.

**Strategic Request Handling Features**

- Dependencies: Reuse logic (like authentication or DB sessions) across multiple endpoints using the Dependency Injection system.
- Middlewares: Process every request before it reaches an endpoint, useful for CORS, logging, or modifying headers.
- Error Handling: Use HTTPException to return standard error responses or define custom exception handlers to override default validation errors.
- Request State: Use request.state to store and share data between middleware and route handlers during a single request lifecycle.

---

## Defining Routes and HTTP Methods

In FastAPI, you define routes using decorators on Python functions. These decorators specify the URL path and the HTTP method used to communicate with that path.

- A route consists of a path, an HTTP method, and a handler function.
- FastAPI provides decorators for all standard HTTP methods. By convention, they are used for specific actions:
  - @app.get(): To read data. No server-side changes should occur.
  - @app.post(): To create data, such as adding a new record to a database.
  - @app.put(): To update or replace an entire resource.
  - @app.patch(): To apply partial updates to an existing resource.
  - @app.delete(): To remove data permanently.
  - Others: @app.options(), @app.head(), @app.trace()

- You can capture dynamic values from the URL by using curly braces {} in the path.
  - Type Validation: Use Python type hints in the function signature. FastAPI automatically converts the path segment to that type (e.g., int) and returns a 422 Unprocessable Entity error if validation fails.
  - Order of Routes: FastAPI matches routes in the order they are defined. Always place fixed paths (e.g., /users/me) before dynamic paths (e.g., /users/{user_id}) to avoid the fixed path being caught by the dynamic parameter.

- For larger applications, use the APIRouter class to organize routes into different files.
  - Prefixes and Tags: Group related routes under a common URL prefix (e.g., /users) and tag them for organization in the Swagger UI interactive documentation.

- Response Status Codes: You can define the default HTTP status code (e.g., 201 for success) using the status_code parameter in the decorator.
- Exclusion: Use include_in_schema=False to hide a route from the OpenAPI documentation.

---

## Path Parameters

In FastAPI, path parameters are dynamic parts of a URL used to identify specific resources. They are defined using curly braces in the route path and captured as function arguments.

You declare path parameters by adding them to the path string and then defining them as arguments in your function.

- Automatic Validation: FastAPI uses Python type hints to automatically validate data. If a parameter is declared as an int but a string is provided, FastAPI returns a 422 Unprocessable Entity error.
- Editor Support: Type hints provide autocompletion and error checking within your code.
- Predefined Values (Enums): To restrict a path parameter to specific allowed values, use a Python Enum. FastAPI will validate that the input matches one of the enum members.
- Path Converters: If a path parameter needs to contain its own path (e.g., /files/{file_path:path}), you can use the converter to capture everything after the slash, including additional slashes.
- Numeric Validation: Using the Path class (often via Annotated), you can add numeric constraints like gt (greater than), ge (greater than or equal), lt (less than), or le (less than or equal).

**Key Characteristics**

- Required: Unlike query parameters, path parameters are always required because they are part of the URL structure.
- Order Matters: Define more specific routes (like /users/me) before generic routes (like /users/{user_id}) to prevent the generic route from "shadowing" the specific one.
- Documentation: Path parameters are automatically included in the Swagger/OpenAPI documentation generated at /docs.

---

## Query Parameters

Query parameters in FastAPI are the key-value pairs that appear after the ? in a URL (e.g., /items/?skip=0&limit=10). In FastAPI, any function parameter that is not part of the path is automatically interpreted as a query parameter.

**Basic Declaration**
To define a query parameter, simply add it as a keyword argument in your path operation function. FastAPI automatically converts types (e.g., from string to integer) and validates the data.

- Required Parameter: Declare the parameter without a default value.
- Optional Parameter: Assign a default value (like None or a specific string/number).

**Advanced Validation and Metadata**
Use the Query class (imported from fastapi) to add constraints and documentation metadata.

- Constraints: min_length, max_length, pattern (regex), gt (greater than), le (less than or equal).
- Metadata: title, description, alias (for parameter names that are invalid Python identifiers), and deprecated=True.

**Multiple Values (Lists)**
To receive multiple values for the same parameter (e.g., /items/?q=foo&q=bar), declare the type as a list and explicitly use Query().

**Query Parameter Models**
For endpoints with many parameters, you can group them into a Pydantic model. This makes the code cleaner and the parameters reusable across different routes.

**Common Patterns and Best Practices**

- Boolean Conversion: FastAPI intelligently converts values like "true", "1", "on", or "yes" (case-insensitive) to the Python boolean True.
- Enum Integration: Use Python Enum to restrict query parameters to a specific set of valid options, which will also appear as a dropdown in the Swagger UI.
- Keyword-Only Arguments: If you have many parameters, use \* in the function signature to force keyword-only arguments, preventing ordering issues.
- Documentation: All declared query parameters are automatically added to the interactive API documentation at /docs.

---

## Request and Response Models

FastAPI utilizes Pydantic models to define the structure of data entering and leaving your API. These models ensure that data is validated, type-converted, and properly documented in the FastAPI automatic interactive docs.

**Request Models (Input)**
Request models define the expected structure of the data sent by the client in the request body.

- Declare a class inheriting from pydantic.BaseModel.
- Pass the model as a type hint in your path operation function's parameters.

**Features:**

- Automatic Validation: FastAPI checks incoming JSON against the model's types and constraints (e.g., min_length). If invalid, it returns a 422 Unprocessable Entity error automatically.
- Data Parsing: Automatically converts JSON data into a Python object you can interact with directly.
- Example: async def create_user(user: UserCreate): will expect a JSON body matching the UserCreate schema.

**Response Models (Output)**
Response models define the structure of the data your API sends back to the client.
Declaration: Use the response_model parameter in the path operation decorator (e.g., @app.get("/", response_model=UserOut)).

**Functions:**

- Data Filtering: Automatically removes fields not defined in the response model (e.g., hiding hashed passwords or internal database IDs).
- Data Conversion: Formats complex types like datetime or UUID into standard JSON-friendly strings.
- Security: Acts as a "gatekeeper" to ensure sensitive internal data is never leaked to the public.
- Performance: Using a response_model allows FastAPI to use highly optimized Pydantic serialization, which is faster than manual conversion.

**Best Practices: Separation of Concerns**
It is highly recommended to use separate models for requests and responses rather than a single shared model.

- Request Model: Includes fields the client must provide (e.g., password, email).
- Response Model: Includes fields the server generates (e.g., id, created_at) and excludes sensitive ones (e.g., hashed_password).
- DRY Principle: Use class inheritance to share common fields (e.g., a UserBase class containing email and full_name inherited by both UserCreate and UserOut).

**Advanced Response Control**

- Excluding Defaults: Use response_model_exclude_unset=True to only return values that were explicitly set, hiding default values from the JSON output.
- Dynamic Filtering: You can use response_model_include or response_model_exclude to dynamically pick fields to send, though separate models are generally preferred for clarity.
- Multiple Status Codes: You can define different models for different HTTP status codes using the responses parameter.

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

Pydantic is the foundational data handling engine for FastAPI, providing the mechanism for data validation, parsing, and serialization. By defining Pydantic models (classes inheriting from BaseModel), developers establish a clear "contract" for the data entering and leaving an API.

**Core Functions in FastAPI**

- Request Data Validation: FastAPI uses Pydantic to check that incoming request bodies (JSON) match the expected types and structures. If the data is invalid, it automatically returns a detailed 422 Unprocessable Entity error to the client.
- Data Parsing and Coercion: Pydantic automatically converts incoming data into the correct Python types. For example, a string like "123" sent for an integer field will be automatically coerced into the integer 123.
- Response Shaping and Filtering: Using the response_model parameter in path decorators allows FastAPI to filter out sensitive or unnecessary fields from the output. This ensures the client only receives what is explicitly defined in the model.
- Automatic Documentation: Pydantic models automatically generate JSON Schemas, which FastAPI then uses to populate interactive documentation like Swagger UI and ReDoc.
- Complex Constraints: Beyond simple type checking, Pydantic Field allows for complex validation rules, such as minimum/maximum values, string patterns (regex), and list length requirements.

**Key Performance Benefits**

- Pydantic V2 is written in Rust, making it one of the fastest data validation libraries available for Python.
- TBecause Pydantic is based on standard Python type hints, it provides excellent IDE support, including auto-completion and static analysis, reducing runtime bugs.
- FastAPI is built directly on top of Pydantic, meaning any advanced Pydantic feature (like BaseSettings for configuration management) works natively within the framework.

---

## Asynchronous Programming in FastAPI

Asynchronous programming uses `async`/`await` to handle many concurrent requests efficiently.

**What is Asynchronous Programming and how do we use it?**

- **async def:** Declares an asynchronous function.
- **await:** Yields control while waiting for I/O.
- **I/O-bound operations:** Ideal for async (network, disk, DB).
- **Event loop:** Manages and schedules async tasks.

**How do we implement it?**

- I/O-Bound Operations: Use async-compatible libraries to maintain performance.
- HTTP Requests: Use HTTPX instead of requests.
- Databases: Use drivers like asyncpg (PostgreSQL) or motor (MongoDB).
- Mixing Sync and Async: If you must run a blocking function inside an async route, use anyio.to_thread.run_sync or asyncio.to_thread to prevent stalling the event loop.
- Background Tasks: For tasks that don't need to finish before sending a response (e.g., sending an email), use FastAPI's built-in BackgroundTasks.

**When to Use async**

- Database queries with async drivers.
- External API calls using an async client like HTTPX.
- Asynchronous file handling with `aiofiles`.

**When to Use def**

- CPU-intensive calculations.
- Blocking libraries that do not support async.

**What are some common pitfalls?**

- Forgetting await: If you call an async function without await, it returns a coroutine object instead of the result.
- Blocking the Loop: Using time.sleep() or heavy math inside async def stops FastAPI from handling any other requests until that task is done.

---

## Database Integration

FastAPI integrates with both SQL and NoSQL databases through third-party libraries. It uses a dependency injection system to manage database sessions, ensuring they are opened and closed correctly for every request.

**SQL Databases (Relational)**
The most common approach for SQL databases (PostgreSQL, MySQL, SQLite) is using SQLAlchemy or SQLModel.

- SQLModel: Designed by the creator of FastAPI, it combines SQLAlchemy and Pydantic into one tool, reducing code duplication.
- SQLAlchemy: The industry standard for Python ORMs. It allows you to interact with databases using Python classes instead of raw SQL.

**How do we setup?**

- Define a Database URL: For example, postgresql://user:password@postgresserver/db.
- Create an Engine: This is the actual connection to the database.
- Create a SessionLocal Class: Each instance of this class will be a database session.
- Define Models: Use a Base class to create table schemas.
- Create a Dependency: Use a get_db function with yield to provide a database session to your API routes and ensure it closes automatically.

**NoSQL Databases**
For NoSQL options like MongoDB, integration typically uses PyMongo or an asynchronous driver like Motor.

**MongoDB Integration:**

- Use Pydantic models to define the data structure and perform validation.
- Connect using a client like AsyncMongoClient for non-blocking operations.
- Manage the connection lifecycle using lifespan events (startup and shutdown) to ensure the database client is correctly initialized and closed.

**What are some key best practices?**

- Environment Variables: Never hardcode credentials. Use tools like python-dotenv or the built-in Pydantic Settings to manage DATABASE_URL.
- Migrations: For production SQL databases, use Alembic to manage schema changes over time.
- Async Support: For high-concurrency needs, use asynchronous drivers (e.g., asyncpg for PostgreSQL or Motor for MongoDB) to prevent blocking the event loop.
- Interactive Documentation: Once integrated, your database models will automatically reflect in the Swagger UI (typically at /docs), allowing you to test CRUD operations immediately.

---

## Security and Authentication

FastAPI provides a modular security system built on top of Python Type Hints and Dependency Injection, allowing you to implement industry-standard protocols like OAuth2 and JWT with minimal boilerplate.

**What are some core Authentication Methods?**
FastAPI supports several security schemes that integrate directly with the interactive OpenAPI documentation (/docs).

- OAuth2 with Password Flow & JWT: The recommended standard for most production web applications. It uses a "password flow" to exchange credentials for a short-lived JSON Web Token (JWT).
- HTTP Basic Auth: Sends a username and password in every request header. Best for internal tools or quick prototypes. Use HTTPBasic and HTTPBasicCredentials from fastapi.security.
- API Key Authentication: Involves a static key passed in the header, query parameter, or cookie.
- OpenID Connect (OIDC): Used for "Login with Google/GitHub" integrations. It acts as an identity layer on top of OAuth2.

**Implementation Workflow**
To secure your API, follow this general dependency-based pattern:

- Define Security Scheme: Instantiate a security class like OAuth2PasswordBearer or HTTPBasic.
- Create Dependency Function: Write a function that uses the security scheme to extract credentials (e.g., a token or username/password).
- Validate Credentials: In your dependency, verify the token signature (for JWT) or check the database for the user.
- Inject into Routes: Use Depends() to protect specific endpoints.

**Security Best Practices**

- Password Hashing: Never store plain-text passwords. Use libraries like passlib with the bcrypt algorithm to hash passwords before saving them.
- Use HTTPS: All authentication methods are insecure if transmitted over plain HTTP. Always use HTTPS in production.
- Short-lived Tokens: Set JWT expiration (e.g., 15-60 minutes) to minimize damage if a token is stolen.
- Secure Credential Comparison: Use secrets.compare_digest() to prevent timing attacks when comparing sensitive strings.
- Fine-Grained Authorization: Use OAuth2 Scopes with Security() instead of Depends() to restrict specific endpoints based on user permissions.

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

**References:**

1. [FastAPI Documentation](https://fastapi.tiangolo.com/)
