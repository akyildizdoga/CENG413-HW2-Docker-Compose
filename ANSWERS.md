# CENG413 HW-2: Written Answers

## 1. Service Name Resolution

Docker Compose creates a shared network for the services. My Flask application connects to Redis using the service name `cache`, which Docker resolves to the Redis container's IP address through its internal DNS. This allows the containers to communicate without using fixed IP addresses or `localhost`. On the default Docker bridge network used by ordinary `docker run` commands, automatic container-name DNS resolution is not provided in the same way.

## 2. Stateless Application and Data Persistence

My Flask application is stateless because the visit counter is stored in Redis instead of the application container. I removed the app container using `docker compose rm -sf app` and recreated it with `docker compose up -d`; the counter continued from its previous value. I also tested `docker compose down` and restarted the services, and the Redis data remained available. Finally, I used `docker compose down -v`, which removed the named volume, and the counter restarted from 1.

## 3. Passwords and Repository Security

Database passwords should come from environment variables or a secure secrets management system rather than being written directly in source code. For Docker Compose, a local `.env` file can provide the password, and this file should be excluded from Git using `.gitignore`. An `.env.example` file can contain fake values to show which variables are required. Committing passwords to Git is dangerous even in private repositories because credentials may be exposed through repository access, copied files, or Git history.

## AI Assistant Usage

I used an AI assistant to understand Docker Compose commands, troubleshoot the setup, and help organize my written explanations. I ran the commands myself and verified the application behavior using Docker Desktop, VS Code, and my browser.