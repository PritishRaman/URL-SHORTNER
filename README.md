# URL Shortener

A full-stack URL shortening application built with **Java, Spring Boot, React, MySQL, and Redis**. The application supports user authentication, short-link creation, redirect handling, and click tracking.

## Overview

This project provides a web interface for creating and managing shortened URLs. The backend exposes REST APIs, uses JWT-based authentication, stores URL data in MySQL, and uses Redis for caching and rate limiting.

The frontend is built with React and Vite and communicates with the Spring Boot API.

## Features

- **URL Shortening:** Generate short codes for long URLs.
- **User Authentication:** Registration and login using JWT.
- **Link Management:** View and manage shortened URLs.
- **Click Tracking:** Track visits to shortened links.
- **Redis Caching:** Cache redirect lookups to reduce database reads.
- **Rate Limiting:** Limit incoming requests using Redis.
- **AI Categorization:** Optional URL categorization through the Groq API.
- **Database Migrations:** Manage schema changes with Flyway.
- **Docker Support:** Run the backend and supporting services using Docker Compose.
- **Automated Checks:** GitHub Actions workflow for testing and building.

## Technology Stack

| Component | Technology |
|---|---|
| Backend | Java 21, Spring Boot |
| Security | Spring Security, JWT, BCrypt |
| Frontend | React, Vite, React Router, Axios |
| Database | MySQL 8, Flyway |
| Cache and rate limiting | Redis |
| AI integration | Groq API |
| Testing | JUnit 5, Mockito, Testcontainers |
| Deployment tooling | Docker, Docker Compose |
| CI | GitHub Actions |

## Project Structure

```text
url-shortener/
├── src/                         # Spring Boot backend
├── url-shortener-frontend/      # React frontend
├── .github/workflows/           # CI configuration
├── pom.xml                      # Maven configuration
├── Dockerfile
├── docker-compose.yml
├── .env.example
└── README.md
```

## Prerequisites

- Docker Desktop with Docker Compose
- Node.js 20 or later
- Git

## Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/PritishRaman/URL-SHORTNER.git
cd URL-SHORTNER
```

### 2. Configure environment variables

Create a local environment file:

```powershell
Copy-Item .env.example .env
```

Set the database credentials and a secure JWT secret in `.env`. Keep this file private and do not commit it to Git.

### 3. Start the backend services

```bash
docker compose up --build
```

The API should be available at:

`http://localhost:8080`

### 4. Start the frontend

Open a second terminal:

```bash
cd url-shortener-frontend
npm install
npm run dev
```

Open the local URL printed by Vite, usually:

`http://localhost:5173`

Keep the backend running while using the frontend.

## API Overview

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/auth/register` | Register a user |
| POST | `/api/auth/login` | Authenticate a user |
| POST | `/api/urls` | Create a shortened URL |
| GET | `/{shortCode}` | Redirect to the original URL |
| GET | `/api/urls/{shortCode}/analytics` | Retrieve click analytics |
| GET | `/actuator/health` | Check backend health |

Authenticated endpoints require a valid bearer token where applicable.

## Configuration

| Variable | Purpose |
|---|---|
| `DB_ROOT_PASSWORD` | MySQL root password |
| `DB_USER` | Application database username |
| `DB_PASSWORD` | Application database password |
| `JWT_SECRET` | Secret used to sign JWTs |
| `BASE_URL` | Base URL used to construct short links |
| `AI_TAGGING_ENABLED` | Enable or disable AI categorization |
| `GROQ_API_KEY` | API key for AI categorization |
| `FORWARD_HEADERS_STRATEGY` | Configure trusted-proxy header handling |

Use `.env.example` as the configuration template. Use unique secrets for every deployment environment.

## Testing

Run backend tests from the project root:

```bash
mvn test
```

Tests that use Testcontainers require Docker to be running.

## Future Improvements

- Add a custom-alias option for short links.
- Improve the dashboard and mobile layout.
- Add richer click analytics and visualizations.
- Add production deployment configuration.
- Expand automated testing for frontend workflows.

## License and Attribution

This project is based on an existing URL shortener codebase. Refer to the included `LICENSE` file and original project history for applicable license terms and attribution.


