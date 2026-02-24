In this DevOps task, i built and deployed a full-stack CRUD application using the MEAN stack (MongoDB, Express, Angular 15, and Node.js). The backend will be developed with Node.js and Express to provide REST APIs, connecting to a MongoDB database. The frontend will be an Angular application utilizing HTTPClient for communication.  

The application will manage a collection of tutorials, where each tutorial includes an ID, title, description, and published status. Users will be able to create, retrieve, update, and delete tutorials. Additionally, a search box will allow users to find tutorials by title.

## Containerization with Docker

This project is fully containerized using Docker and Docker Compose.

### Local Setup

To run the entire stack locally:

1. Ensure you have Docker and Docker Compose installed.
2. Run the following command in the root directory:
   ```bash
   docker-compose up --build
   ```
3. The frontend will be accessible at `http://localhost`.
4. The backend API will be at `http://localhost/api`.
5. MongoDB will be running on port `27017`.

## Deployment to Ubuntu VM

### 1. Prerequisites
- An Ubuntu VM (AWS EC2, Azure VM, etc.).
- Docker and Docker Compose installed on the VM.
- Port 80 (HTTP) open in the VM's security group/firewall.

### 2. CI/CD Pipeline (GitHub Actions)
The project includes a GitHub Actions workflow in `.github/workflows/main.yml`. To enable it:

1. Create a new GitHub repository and push this code.
2. In your GitHub Repo, go to **Settings > Secrets and variables > Actions**.
3. Add the following secrets:
   - `DOCKER_USERNAME`: Your Docker Hub username.
   - `DOCKER_PASSWORD`: Your Docker Hub personal access token or password.
   - `SSH_HOST`: The public IP address of your VM.
   - `SSH_USER`: The username for the VM (usually `ubuntu`).
   - `SSH_PRIVATE_KEY`: Your private SSH key (`.pem` file content) used to access the VM.

### 3. VM Preparation
On your VM, create the target directory:
```bash
mkdir -p ~/crud-dd-task-mean-app
```
And copy the `docker-compose.yml` and `nginx/nginx.conf` to the VM (The CI/CD script assumes they are in that folder). 

## Nginx Reverse Proxy
Nginx is configured to:
- Serve the Angular static files.
- Proxy all `/api` requests to the Node.js backend on port 8080.
- Handle SPA routing (redirecting 404s to `index.html`).

---
Finalized for deployment on February 24, 2026.

SSH FIX DONE
