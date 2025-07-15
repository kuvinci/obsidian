#linux #php #server
# ✅**Phase 0: Roadmap Preview**
Here's the high-level roadmap (and you can adjust it as we go):
1. **How HTTP Servers Work: The Big Picture**
    - Requests, responses, TCP/IP, sockets, ports, processes, event loops.
    - Why (and how) Nginx/Apache work as proxies.
2. **TCP & HTTP Protocol Basics
    - How a web server “talks” on the network (sockets in PHP).
    - Parsing raw HTTP requests.
    - Responding with valid HTTP.
3. **Building a Barebones HTTP Server in PHP
    - Code modularity
	- Separation of concerns (request parsing, response building, routing, etc.)
	- Extensible architecture (making it easy to grow later)
	- Dependency injection and config management
	- Best practices for maintainable code
    - Using PHP’s socket extension (step-by-step).
    - Handling requests/responses.
    - Serving static files.
    - Serving dynamic PHP (hello world from your own server!).
4. **Security Foundations
    - Secure defaults: minimal attack surface.
    - Handling malformed input, directory traversal, etc.
    - Rate limiting and basic logging.
5. **Serving HTTPS (SSL/TLS)
    - SSL/TLS theory: what really happens.
    - Using OpenSSL with PHP sockets.
    - Generating and using self-signed certs.
    - Security pitfalls in HTTPS handling.
6. **Reverse Proxy: Nginx/Apache in Front**
    - Why use a reverse proxy.
    - Offloading SSL, static files, caching.
    - Real-world production setups (your PHP server behind Nginx).
7. **Extending Your Server
    - Simple routing, middleware, etc.
    - Deploying Laravel/static/other projects.
8. **Bonus: Dockerizing & Deployment
    - Writing a Dockerfile for your server.
    - Exposing ports, networking tips.
    - (Optional) Supervising your process.
9. **Hardening and Maintaining**
    - Keeping the server up-to-date.
    - Monitoring, logging, failover basics.


## What _really_ happens when you open `https://yourdomain.com/` in your browser:
- **DNS resolution:** Browser asks DNS for the IP of `yourdomain.com`
- **TCP connection:** Browser connects to server's IP on port 80 (HTTP) or 443 (HTTPS)
- **TLS handshake:** If HTTPS -> browser negotiates an encrypted CHANNEL (SSL/TLS)
- **HTTP request sent:** Browser sends an HTTP request (GET/POST/PUT/etc.) to the server:
```http
GET / HTTP/1.1
Host: yourdomain.com
User-Agent: Mozilla/5.0 ...
Accept: text/html,application/xhtml+xml,...
```
- Server reads request: parses from the TCP socket
- Server processes request:
	- Serving a static file (index.html, image.png)
	- OR Executing a script (like Laravel’s index.php)
	- OR Returning an error (404, 500, etc.)
- HTTP response sent:
```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 42
```
- **Connection closes or kept-alive:** TCP socket is closed, or kept open for more requests.

## What does a real HTTP server need to handle:
- **Networking: ports, multiple connections, timeouts**
- **Protocol parsing: Parse HTTP**
- **Routing**
- **Serve static files from disk with caching**
- **Run scripts or apps**
- **Protect against attacks**
- **Logging & Monitoring**
- **Concurrency**

## How to achieve Concurrency:
- **Multi-Process:** Apache, PHP-FPM
- **Multi-Threaded:** Not available in PHP
- **Async/Event Loop:** One process, non-blocking IO (Node.js, Nginx, Swoole)
- OR Hybrid: Mix of above (Nginx with worker processes)
Classic PHP apps are "stateless" -> good for isolation, bad for speed if not careful

## Why use reverse proxies (e.g., Nginx/Apache in front)?
- Terminates SSL/TLS, handles slow clients, offloads static files
- Forwards dynamic requests (PHP, Node.js, etc.) to backend servers
- Adds load balancing, caching, rate limiting

## Web flow digram
```sql
+-------------------+       TCP/HTTP/S    +-------------------+       PHP app/Script
|  Your Browser     |  <===============>  |  Your HTTP Server |  <=>  (Laravel, etc.)
+-------------------+                    +-------------------+
                                                ^
                                                |
                                        [Maybe] Reverse Proxy (Nginx)
```

