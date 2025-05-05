# Client Server Model %% fold %%

- The **Client-Server Model** is a **computing architecture** where, a **client** requests services, and a **server** provides them.

## Components of the Client-Server Model %% fold %%

### a) Client

- **Requesting entity** that interacts with the server.
- Sends **requests** and waits for a **response**.
- **Examples**: web browser, mobile app, desktop application, or IoT device.

### b) Server

- **Providing entity** that processes client requests.
- Stores, manages, and delivers **data, resources, or services**.
- **Examples**:
    - **Web servers** (Apache, Nginx).
    - **Database servers** (MySQL, MongoDB).
    - **Application servers** (Node.js, Java).

### c) Network

- **Medium** through which the client and server communicate.
- Uses **protocols** such as **HTTP, FTP, SMTP, TCP/IP**.
- **Examples**: (LAN, WAN, Internet).

---

## Client-Server Model Mechanism %% fold %%

1. **Client initiates a request** (e.g., loading a website).
2. **Request is sent** via a network to the server.
3. **Server processes** the request (e.g., fetching data from a database).
4. **Server sends a response** back to the client.
5. **Client receives and displays the response** (e.g., rendering a webpage).

![[Mechanism.png]]

---

## Types of Client-Server Architecture %% fold %%

![[Client Server Models.png]]

### **a) Two-Tier Architecture**

- Direct communication between **client** and **server**.
- Example: A **desktop app** directly connected to a **database**.

### **b) Three-Tier Architecture** _(Most Common)_

- Introduces an **Application (Middleware) Server** between Client and Database Server.
- Example:
    - **Client** : Web Browser (React)
    - **Middleware** : Express.js (Handles requests)
    - **Database** : MongoDB (Stores data)

### **c) Multi-Tier (N-Tier) Architecture**

- Includes **Load Balancers, Caching Layers, Microservices**.
- Used in **enterprise-level applications** like e-commerce, banking systems.

---

## Advantages and Disadvantages of Client-Server Model %% fold %%

| **Advantages**                                                    | **Disadvantages**                                                                         |
| :---------------------------------------------------------------- | :---------------------------------------------------------------------------------------- |
| ✅ **Centralised Management:**<br>Easier to monitor & update.     | ❌ **Single Point of Failure:**<br>If the server crashes, clients cannot access services. |
| ✅ **Scalability:**<br>Servers can handle multiple clients.       | ❌ **Network Dependency:**<br>Performance depends on network stability.                   |
| ✅ **Security:**<br>Controlled access to resources and data.      | ❌ **Scalability Costs:**<br>High-traffic servers require expensive infrastructure.       |
| ✅ **Data Integrity:**<br>Centralised storage reduces redundancy. |                                                                                           |

---

## Client-Server vs Peer-to-Peer (P2P) %% fold %%

> [!tip]+ (P2P) : Peer-to-Peer Model
>
> -   **Peer-to-Peer (P2P) Model** is a decentralized network architecture where each computer or device (referred to as a "peer") can **act both as a client and a server.**
> -   This means that peers can directly share resources (like files, processing power, or internet connections) with each other without the need for a central server.

| Feature         | Client-Server                   | Peer-to-Peer (P2P)            |
| --------------- | ------------------------------- | ----------------------------- |
| **Control**     | Centralised                     | Decentralised                 |
| **Security**    | Higher                          | Lower                         |
| **Performance** | High but depends on server load | Distributed but may be slower |
| **Examples**    | Websites, Cloud Services        | Torrenting, Blockchain        |

---

# Web Requests (HTTP methods) %% fold %%

- **Web requests** are different ways servers **communicate** with other servers to **exchange data**.
- It is a message sent **from a client** - **to a server** asking for information or to perform an action.
- Example: **Loading a webpage**, **submitting a form**, or **fetching data from an API**.

> [!info]+ HTTP / HTTPS & URL / URI
>
> ### **HTTP** ( _HyperText Transfer Protocol_ ):
>
> -   It defines how messages are formatted and transmitted on the web, and how web servers and browsers should respond to various commands.
>
> ---
>
> ### **HTTPS** ( _HyperText Transfer Protocol Secure_ ):
>
> -   The secure version of HTTP.
> -   It **encrypts** the data exchanged between the user's browser and the web server using **SSL/TLS** protocols.
> -   This ensures **confidentiality**, **integrity**, and **security** for sensitive data.
>
> ---
>
> ### **URL** ( _Uniform Resource Locator_ ) :
>
> -   **Web address** used to access resources on the internet, like websites, images, videos, files, and more.
>
> ---
>
> ### **URI** ( _Uniform Resource Identifier_ ):
>
> -   A **URI** is a string of characters used to **identify** a resource either **by location**, **by name**, or **both**.

## Types of Web Requests (HTTP Methods) %% fold %%

| **Method**  | **Purpose**                                | **Common Use Case**                                       |
| ----------- | ------------------------------------------ | --------------------------------------------------------- |
| **GET**     | Requests data from a server                | Loading a webpage, fetching data                          |
| **POST**    | Sends data to the server                   | Submitting forms, creating data                           |
| **PUT**     | Updates existing data on the server        | Updating user profile, replacing resources                |
| **DELETE**  | Removes data from the server               | Deleting an account, removing items                       |
| **PATCH**   | Partially updates data                     | Updating part of a resource, like changing a single field |
| **HEAD**    | Retrieves only headers (metadata)          | Checking if a resource exists, caching validation         |
| **OPTIONS** | Asks the server what methods are supported | CORS preflight requests, discovering allowed operations   |

---

## Structure of an HTTP Request %% fold %%

An HTTP request typically includes:

- **Request Line :** Method (e.g., GET), URL, HTTP version.
- **Headers :** Key-value pairs that provide **metadata** about the request, such as content type, authorization tokens, etc.
- **Body** (_Optional_) : Data sent with the request, usually in POST/PUT requests.

Example of a GET request in bash(shell):

```bash
GET /api/v1/data HTTP/1.1
```

## Handling Responses %% fold %%

A server responds with:

- **Status Code:** Indicates the result (e.g., 200 OK, 404 Not Found, 500 Internal Server Error).
- **Headers:** Metadata about the response.
- **Body:** The actual content (HTML, JSON, etc.).

```bash
HTTP/1.1 200 OK
```

---

## Web Requests in Different Environments %% fold %%

> [!info]+ Using cURL (cmd)
>
> ```cmd
> curl -X GET https://api.example.com/data
> ```

> [!info]+ In Python (using `requests` library)
>
> ```
> import requests
> response = requests.get('https://api.example.com/data')
> print(response.text)
> ```

> [!info]+ In JavaScript (using `fetch` function)
>
> ```
> fetch('https://api.example.com/data')
> 	.then(response => response.json())
> 	.then(data => console.log(data));
> ```

---

# API %% fold %%

- **API** (_Application Programming Interface_):
    Set of rules that allows software applications to communicate with each other.
- They **enable data exchange** between a client (frontend) & a server (backend).

## Types of APIs %% fold %%

### 1. Web APIs

- **REST API** (_Representational State Transfer_):
    Uses HTTP methods (GET, POST, PUT, DELETE).
- **GraphQL** (Graph Query Language):
    Allows fetching specific data with a single request.
- **WebSockets**:
    Enables real-time communication (e.g., chat apps, live notifications).

### 2. Local APIs

Used within a system for internal communication (e.g., Windows API, Linux system calls).

### 3. Third-Party APIs

Provided by external services (e.g., Google Maps API, Stripe API for payments).

### 4. Open, Private & Partner APIs

- **Open APIs:** Publicly available (e.g., OpenWeather API).
- **Private APIs:** Restricted for internal use (e.g., company's backend services).
- **Partner APIs:** Shared between specific organisations (e.g., Uber integrating Google Maps).

---

## API Response Codes (Status Codes) %% fold %%

| Status Code                        | Meaning              | Example                   |
| ---------------------------------- | -------------------- | ------------------------- |
| ~={green}200=~ OK                  | Success              | Data fetched successfully |
| ~={green}201=~ Created             | Resource created     | New user added            |
| ~={yellow}400=~ Bad Request        | Invalid input        | Missing required fields   |
| ~={yellow}401=~ Unauthorized       | Invalid credentials  | Login failure             |
| ~={yellow}403=~ Forbidden          | No access permission | Restricted data           |
| ~={yellow}404=~ Not Found          | Resource not found   | Wrong URL                 |
| ~={red}500=~ Internal Server Error | Server failure       | Database issue            |

> [!note] Status Code Meanings
>
> -   2\*\* = ~={green}All OK=~
> -   4\*\* = ~={yellow}You messed up=~
> -   5\*\* = ~={red}Server Failed=~

---

# REST APIs %% fold %%

- A **REST API (Representational State Transfer API)** is a **web service** that allows communication between a client (frontend) and a server (backend) using standard HTTP methods.
- REST APIs follow a **stateless architecture** and use JSON or XML for data exchange.

## Principles of REST APIs %% fold %%

| Principle                         | Description                                                                                                                                           |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Statelessness**              | Each request is **independent** (server doesn't store session data).<br>Hence, the client must send **all necessary data** with **each request**.<br> |
| **2. Cacheable**                  | Responses can be **cached** to improve performance.<br>Server must explicitly define if a response needs to be cached.                                |
| **3. Layered System**             | REST APIs can have **multiple layers** (intermediary servers) between the client and the server.                                                      |
| **4. Uniform Interface**          | It has a **uniform and consistent** way of interacting with resources.<br>( http methods, naming conventions, etc.)                                   |
| **5. Client-Server Architecture** | REST APIs follow a **client-server** model.                                                                                                           |

---

## HTTP Methods in REST APIs %% fold %%

| HTTP Method | Action                 | Typical Use Case                               |
| ----------- | ---------------------- | ---------------------------------------------- |
| GET         | Retrieve data          | Fetch resource                                 |
| PUT         | Update resource        | Update existing resource                       |
| POST        | Create resource        | Create new resource                            |
| PATCH       | Partially update       | Partially update resource                      |
| DELETE      | Delete resource        | Delete existing resource                       |
| HEAD        | Retrieve headers       | Get metadata (headers) without body            |
| OPTIONS     | Get allowed methods    | Query available HTTP methods for a resource    |
| TRACE       | Trace the request path | Trace the request path for diagnostic purposes |
| CONNECT     | Establish a tunnel     | Set up a tunnel (mostly for HTTPS proxies)     |

---

## URL Structure %% fold %%

- **Full API URL:**

```http
https://api.example.com/users/1
```

- **Base URL:**

```http
https://api.example.com
```

- **Endpoint URL:**

```http
/users
```

---

## Examples %% fold %%

### GET Request (Fetching Data) %% fold %%

#### Request:

```http
GET /users/1 HTTP/1.1
Host: api.example.com
Authorization: Bearer <token>
```

#### Response:

```json
{
	"id": 1,
	"name": "John Doe",
	"email": "john@example.com"
}
```

---

### POST Request (Creating Data) %% fold %%

#### Request:

```http
POST /users HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer <token>
```

#### Body:

```json
{
	"name": "Jane Doe",
	"email": "jane@example.com"
}
```

#### Response:

```json
{
	"id": 2,
	"name": "Jane Doe",
	"email": "jane@example.com",
	"message": "User created successfully"
}
```

---
