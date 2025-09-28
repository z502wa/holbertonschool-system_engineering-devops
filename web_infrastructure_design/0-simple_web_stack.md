0. Simple web stack — one-server LAMP-style setup (Nginx + App + MySQL)

Goal: A single server hosts a website reachable at www.foobar.com (server IP: 8.8.8.8).

------------------------------------------------------------
High-level architecture (one server)

User's browser -- HTTPS (TLS) over TCP/443 or HTTP over TCP/80 --> Nginx (Web server)

One Physical/VM Server (IP: 8.8.8.8):
    - Nginx (Reverse proxy / Static files)
    - Application Server (e.g., Gunicorn/PM2/uWSGI)
    - Application code / files (executed by App server)
    - MySQL Database

DNS:
    A record: www.foobar.com → 8.8.8.8
------------------------------------------------------------

What happens when a user accesses the site:
1. The user types https://www.foobar.com in the browser.
2. DNS resolves www.foobar.com → 8.8.8.8 (A record).
3. Browser opens a TCP connection to 8.8.8.8 on 443 (HTTPS) or 80 (HTTP).
4. Nginx receives the request, serves static assets or forwards to Application Server.
5. Application Server runs the code, queries MySQL, and returns response via Nginx.

------------------------------------------------------------
Components and their roles:
- Server: Physical/virtual machine running software.
- Domain name: Maps human-friendly name to IP.
- DNS record: "www" is an A record pointing to 8.8.8.8.
- Web server (Nginx): Handles HTTP/HTTPS, serves static files, proxies requests.
- Application server: Executes app code and business logic.
- Application files: The source code of the website.
- Database (MySQL): Stores structured data (users, posts, etc.).
- Protocol: HTTP/HTTPS over TCP with TLS for encryption.

------------------------------------------------------------
Issues with this single-server design:
- SPOF (Single Point of Failure): If the server crashes, the whole site is down.
- Maintenance downtime: Restarting Nginx or DB → downtime.
- Cannot scale: One server cannot handle high traffic load.

------------------------------------------------------------
Sources for reference:
- DNS Records (A vs CNAME) – Cloudflare Docs: https://developers.cloudflare.com/dns/manage-dns-records/reference/record-types/
- NGINX — What is NGINX?: https://www.nginx.com/resources/glossary/nginx/
- MySQL Documentation: https://dev.mysql.com/doc/refman/8.0/en/
- HTTP/HTTPS Basics — MDN: https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview
