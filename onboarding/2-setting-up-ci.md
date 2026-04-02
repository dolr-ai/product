# Deployment Guide

This document outlines the standard procedure for deploying our backend services using **Docker** and managing secrets securely through environment variables. You need to wire up your CI pipeline to follow the below steps on every push to the main branch, ensuring that deployments are consistent and secure.

---

## Deployment Overview

All services should be using **Docker** (via `docker-compose`).  
Secrets are injected at runtime using environment variables, ensuring that no sensitive information is stored inside the repository or directly on the server.

---

## Steps for Deployment

### 1. SSH into the Server

```sh
ssh user@your-server-ip
```

### 2. Configure Secrets in `docker-compose.yml`

```yaml
environment:
  SECRET_NAME: ${SECRET_NAME}
```

### 3. Run Docker Compose With Secrets

Pass secrets inline when starting the services:
`SECRET_NAME="secret value" docker-compose up -d`
For multiple secrets:
`SECRET_ONE="value1" SECRET_TWO="value2" docker-compose up -d`


### 4. Persistence Across Reboots
Docker stores resolved environment variables in the container’s configuration when it starts, so secrets remain available after reboot.
Re-enter secrets only if containers are rebuilt or recreated.

### 5. Fetching Secrets

The secrets that you'll use and create need to go into the team Vault maintained at vault.yral.com. Ask Naitik from the team for help on this on the Team Chat channel if you're struggling with this.

### Notes
- Never store secrets in .env files on the server.
- This approach should be configured using CI on every push to main branch.
