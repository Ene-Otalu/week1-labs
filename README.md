# Week 1: Backend Architecture & Container Security

## Security Fixes Applied

* **PostgreSQL:** 
  To secure the database, I removed the default `POSTGRES_PASSWORD` environment variable and replaced it with `POSTGRES_HOST_AUTH_METHOD=scram-sha-256` to enforce strong password encryption. To block external host access, I removed the `ports: - "5432:5432"` directive from the `docker-compose.yml` file. This ensures the database is only accessible internally via the isolated Docker bridge network, completely shielding it from external port scans.

* **Redis:** 
  Out of the box, Redis allows unauthenticated access. I secured this by adding the `command: redis-server --requirepass "MyStr0ngP@ssw0rd!"` directive to enforce authentication. Furthermore, I disabled dangerous administrative commands that an attacker could use to wipe the server or change configurations by passing `--rename-command FLUSHALL ""` and `--rename-command CONFIG ""` during startup.

## Operational Friction Reflection
The broken container exercise taught me that following a clean, "happy path" tutorial creates a false sense of security. When I first ran `docker-compose up`, the PostgreSQL container immediately crashed. Instead of blindly searching Google, I ran `docker logs hardened_postgres`. The logs explicitly told me that the container failed to boot because a critical environment variable for the authentication method was missing, and a port conflict was preventing the binding. 

This friction forced me to realize that containers are not magic boxes; they are just isolated Linux processes that require exact parameters to survive. Reading the raw crash logs shifted my mindset from a passive consumer to an active engineer. I learned that exit codes and error outputs are actually the system's way of giving you the exact blueprint to fix the problem. Moving forward, my first reflex when an asset fails won't be to delete and reinstall it, but to immediately check the logs, isolate the failing layer, and patch the root cause.