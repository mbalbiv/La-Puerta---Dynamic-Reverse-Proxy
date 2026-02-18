<img width="1024" height="1024" alt="project_icon" src="https://github.com/user-attachments/assets/c36d25e4-adfc-4c7b-ac56-1e4097b7b057" />

# 🚪 La Puerta — Dynamic Reverse Proxy

**La Puerta** is a lightweight, configuration-driven reverse proxy server that dynamically routes HTTP requests to backend services using path-based rules.

It is designed to be simple, fast, and flexible, ideal for microservices, development environments.

---

## ✨ Features

- Path-based dynamic routing
- Hot-reloadable configuration (no restart required)
- HTTP & HTTPS backend support
- WebSocket (WS) support with full duplex request and response streaming.
- Detailed logging
- Graceful error handling

---

## 🧠 How It Works

**La Puerta** sits between clients and backend services, intelligently forwarding requests based on routing rules defined in a configuration file.

### 1. Request Reception
- Listens for HTTP requests on a configurable port (default: `3000`)
- Logs each incoming request with timestamp, method, URL, and client IP

### 2. Route Matching
- Extracts the pathname from the requested URL  
- Matches against enabled routes
- Uses **path matching**


### 3. URL Transformation (Path Prefix Routing)

- Uses the configured **path** as a prefix, not a single endpoint
- Forwards all nested subpaths transparently to the target backend
- Removes the matched path prefix and appends the remaining path to the target URL
- Preserves query parameters and deep routes automatically


### 4. Request Forwarding
- Supports HTTP and HTTPS backends
- Preserves HTTP method and request body
- Adds `X-Forwarded-*` headers

### 5. Response Handling
- Streams responses back to the client
- Preserves status codes and headers

### 6. Error Handling
- `404` – No matching route
- `502` – Backend unreachable or timeout

---

## 🔄 Dynamic Configuration

`config.json` is hot-reloaded automatically.  
Only changing the service port requires a restart.

---

## ⚙️ Configuration Example

```json
{
  "service-port": 3002,
  "routes": [
    {
      "path": "/api/users",
      "target": "http://localhost:3007",
      "enabled": true,
      "description": "User service API"
    }
  ]
}
```

---

## 🚀 Getting Started

```bash
git clone https://github.com/Melquiceded/La-Puerta---Dynamic-Reverse-Proxy.git
cd La-Puerta---Dynamic-Reverse-Proxy
npm install
npm run dev
```
