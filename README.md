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

## OAuth2-Proxy Containers

### 1. oauth2proxy (Generic Applications)
This container provides OAuth2 authentication for general applications. It uses Azure AD for user authentication and allows any user with a valid Azure AD account to log in. The configuration uses environment variables for Azure AD client ID, secret, tenant ID, and other settings. All users with valid credentials can access the protected resources.

### 2. oauth2proxy-mgt (Management Applications)
This container is dedicated to management applications and restricts access to users who belong to a specific Azure AD group. The group object ID is set via the `MGT_AAD_GROUP_OBJECT_ID` environment variable. Only users in this group can access management resources, providing an extra layer of security for administrative functions.

## Registering Applications on Azure AD

1. **Log in to Azure Portal**
   - Go to https://portal.azure.com
   - Navigate to "Azure Active Directory" > "App registrations"

2. **Register a New Application**
   - Click "New registration"
   - Enter a name (e.g., "NPM Generic App" or "NPM Management App")
   - Set the redirect URI (e.g., `https://<your-auth-url>/oauth2/callback`)
   - Click "Register"

3. **Get Application (Client) ID and Tenant ID**
   - After registration, copy the "Application (client) ID" and "Directory (tenant) ID"
   - Add these values to your `.env` file

4. **Create a Client Secret**
   - Go to "Certificates & secrets"
   - Click "New client secret"
   - Copy the value and add it to your `.env` file

5. **Find the Group Object ID (for Management App)**
   - Go to "Azure Active Directory" > "Groups"
   - Select the group you want to use for management access
   - Copy the "Object ID" from the group overview
   - Set this value as `MGT_AAD_GROUP_OBJECT_ID` in your `.env` file

## Example .env Entries
```
APP_AAD_CLIENT_ID=your_generic_app_client_id
APP_AAD_CLIENT_SECRET=your_generic_app_client_secret
MGT_AAD_CLIENT_ID=your_management_app_client_id
MGT_AAD_CLIENT_SECRET=your_management_app_client_secret
AAD_TENANT_ID=your_tenant_id
MGT_AAD_GROUP_OBJECT_ID=your_group_object_id
```

## License
See `LICENSE` for details.
