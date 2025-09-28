# 0. Simple web stack — one-server LAMP-style setup (Nginx + App + MySQL)

> Goal: A single server hosts a website reachable at **www.foobar.com** (server IP: **8.8.8.8**).

---

## High-level architecture (one server)

```mermaid
flowchart LR
  U[User's browser] -- "HTTPS (TLS) over TCP/443\nor HTTP over TCP/80" --> N[Nginx (Web server)]

  subgraph One Physical/VM Server (IP: 8.8.8.8)
    N -- "Reverse proxy / Static files" --> A[Application Server (e.g., Gunicorn/PM2/uWSGI)]
    A -- "SQL over TCP/3306" --> D[(MySQL Database)]
    C[(Application code / files)] -. "executed by" .-> A
  end

  DNS[(DNS for foobar.com)]
  DNS -- "A record: www.foobar.com → 8.8.8.8" --> U
