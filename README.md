# Nginx Proxy Manager Docker Setup

This repository provides a sample setup for running Nginx Proxy Manager and supporting services using Docker Compose.

## Prerequisites
- Docker and Docker Compose installed
- Clone this repository

## Configuration
1. **Environment Variables**
   - Edit the `.env` file to set your domain, secrets, and Azure AD credentials.
   - All sensitive and environment-specific values are managed in `.env`.

2. **Volumes**
   - Data and certificates are stored in local folders (`./npm/data`, `./npm/letsencrypt`, etc.).

## Usage

### 1. Configure Environment
Edit `.env` and set values for:
- Domain name
- Azure AD client IDs and secrets
- Cookie secrets
- Database credentials

### 2. Start Services
Run the following command in the project directory:

```sh
docker compose up -d
```

This will start all services in the background.

### 3. Access the Application
- **Nginx Proxy Manager Web UI:**
  - http://localhost:81
- **HTTP/HTTPS Proxy:**
  - http://localhost
  - https://localhost

### 4. Stopping Services
To stop all services:

```sh
docker compose down
```

## Customization
- Change ports, volumes, or service settings in `docker-compose.yaml` as needed.
- Update `.env` for different environments or secrets.

## Security
- Never commit real secrets or credentials to public repositories.
- Use strong secrets for cookies and Azure AD credentials.

## Troubleshooting
- Check logs with:
  ```sh
  docker compose logs
  ```
- Ensure all environment variables in `.env` are set and match those referenced in `docker-compose.yaml`.

## License
See `LICENSE` for details.
