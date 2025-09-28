flowchart TD
    subgraph Internet ["Internet Cloud"]
        User["User's Computer<br/>(Browser)"] --> DNS["DNS System"]
        DNS -->|Returns IP: 8.8.8.8| User
        User -->|HTTP/HTTPS over TCP/IP| Server
    end

    subgraph Server ["Single Server (IP: 8.8.8.8)"]
        Nginx["Web Server<br/>(Nginx)<br/>Port 80/443"] --> AppServer["Application Server<br/>(e.g., Gunicorn, PM2)"]
        AppServer --> AppFiles["Application Files<br/>(Codebase)"]
        AppServer <--> Database["Database<br/>(MySQL)<br/>Port 3306"]
        
        ServerExternal["Incoming Requests"] --> Nginx
        AppServer --> Nginx
        Nginx --> Response["HTTP Response"]
    end

    style Server fill:#e1f5fe
    style Internet fill:#f3e5f5
    style Nginx fill:#c8e6c9
    style AppServer fill:#fff3e0
    style Database fill:#ffcdd2
