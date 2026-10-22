# DevOps Tiny Web API

A lightweight HTTP API built with Node.js and containerized using Docker. This project demonstrates Docker image creation, container management, environment-based configuration, health checks, and Docker Compose.

## Features

- Lightweight HTTP server using Node.js built-in `http` module
- Configurable application message using environment variables
- Health-check endpoint
- JSON responses with appropriate HTTP status codes
- Docker image creation and containerization
- Docker Compose configuration
- Git version control and `.gitignore`

## Tech Stack

- **Runtime:** Node.js
- **Containerization:** Docker
- **Container Orchestration:** Docker Compose
- **Version Control:** Git and GitHub

## Project Structure

```text
devops-web-app/
├── app.js
├── Dockerfile
├── docker-compose.yml
├── package.json
├── package-lock.json
├── test.js
├── .gitignore
├── .env.example
└── README.md
```

## API Endpoints

| Method | Endpoint | Description | Response |
|---|---|---|---|
| GET | `/` | Returns the application message | `200 OK` |
| GET | `/health` | Checks whether the server responds | `200 OK` |
| GET | Any other path | Returns a not-found error | `404 Not Found` |

### Example Responses

**Home endpoint — `/`**

```json
{
  "message": "Hello from DevOps task"
}
```

**Health endpoint — `/health`**

```json
{
  "status": "ok"
}
```

**Unknown endpoint**

```json
{
  "error": "Not found"
}
```

## Prerequisites

Install the following tools:

- [Node.js](https://nodejs.org/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Git](https://git-scm.com/)

Ensure Docker Desktop is running before executing Docker commands.

## Run Locally

Clone the repository:

```bash
git clone https://github.com/mandar-07/devops-web-app.git
cd devops-web-app
```

Install dependencies:

```bash
npm install
```

Start the application using the script configured in `package.json`:

```bash
npm start
```

Open these URLs in your browser:

- Home: http://localhost:3000/
- Health check: http://localhost:3000/health

Stop the server using `Ctrl + C`.

## Run with Docker

### 1. Build the Docker image

```bash
docker build -t devops-tiny-web-app:1.0 .
```

### 2. Start the container

```bash
docker run --rm -d \
  --name devops-tiny-api \
  -p 3000:3000 \
  -e APP_MESSAGE="Hello from Docker" \
  devops-tiny-web-app:1.0
```

For Windows PowerShell, you can also run the command on one line:

```powershell
docker run --rm -d --name devops-tiny-api -p 3000:3000 -e APP_MESSAGE="Hello from Docker" devops-tiny-web-app:1.0
```

### 3. Verify the container

```bash
docker ps
docker logs devops-tiny-api
```

### 4. Test the API

```powershell
Invoke-RestMethod http://localhost:3000/
Invoke-RestMethod http://localhost:3000/health
```

### 5. Stop the container

```bash
docker stop devops-tiny-api
```

The `--rm` flag automatically removes the container after it stops.

## Environment Variables

The application supports the following environment variables:

| Variable | Description | Default |
|---|---|---|
| `PORT` | Port on which the server listens | `3000` |
| `APP_MESSAGE` | Message returned by the home endpoint | `Hello from DevOps task` |

You can pass these variables using Docker's `-e` option or an environment file.

Example `.env` file:

```dotenv
PORT=3000
APP_MESSAGE=Hello from Docker
```

Run the container using the environment file:

```powershell
docker run --rm -d --name devops-tiny-api -p 3000:3000 --env-file .env devops-tiny-web-app:1.0
```

Make sure the image tag matches the image you built.

**Security:** Do not commit `.env` files containing secrets. Use `.env.example` to share safe placeholder configuration.

## Run with Docker Compose

Build and start the services:

```bash
docker compose up --build -d
```

View running services:

```bash
docker compose ps
```

View application logs:

```bash
docker compose logs
```

Follow logs continuously:

```bash
docker compose logs -f
```

Stop and remove the Compose containers and network:

```bash
docker compose down
```

Named volumes, if configured, are retained unless explicitly removed.

## Testing

Run the test script if the project has a test script configured:

```bash
npm test
```

The test setup should verify:

- The home endpoint returns the expected message.
- The health endpoint returns a successful status.
- Unsupported paths return HTTP 404.
- JSON responses contain the expected fields.

## Git Workflow

Check the current branch:

```bash
git branch
```

Check changed files:

```bash
git status
```

Create a feature branch:

```bash
git switch -c feature/tiny-web-api
```

Commit changes:

```bash
git add .
git commit -m "Update tiny web API"
```

Push the branch to GitHub:

```bash
git push -u origin feature/tiny-web-api
```

## Learning Outcomes

Through this project, I practised:

- Building a simple HTTP API using Node.js
- Creating Docker images using a Dockerfile
- Running and managing Docker containers
- Mapping host ports to container ports
- Configuring applications using environment variables
- Running services using Docker Compose
- Testing API endpoints and checking container logs
- Managing project files using Git and GitHub

