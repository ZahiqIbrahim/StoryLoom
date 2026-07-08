# Storyloom
 
Storyloom is a microservices-based platform for discovering, tracking, and discussing books and movies. It combines AI-powered recommendations, a shared catalog sourced from external APIs, and real-time community chat, all behind a single API gateway with centralized authentication.
 
The platform is split into independently deployable Spring Boot services, each registered with Eureka for service discovery and containerized with Docker.
 
## Architecture
 
All services register with Eureka for service discovery and communicate via OpenFeign. The API Gateway is the single entry point, handling JWT validation and routing to each downstream service. Services are containerized together on a shared Docker network.
![Storyloom architecture diagram](docs/architecture.png)
 
## Services
 
| Service | Description | Repo |
|---|---|---|
| API Gateway | Single entry point — JWT validation, routing, CORS, WebSocket proxying | [storyloom-api-gateway](https://github.com/ZahiqIbrahim/storyloom-api-gateway) |
| Auth Service | Registration, OTP email verification, JWT access/refresh tokens, password reset | [storyloom-auth-service](https://github.com/ZahiqIbrahim/storyloom-auth-service) |
| Catalog Service | Book/movie search and trending data via Open Library & TMDB | [storyloom-catalog-service](https://github.com/ZahiqIbrahim/storyloom-catalog-service) |
| Community Service | Real-time chat rooms via WebSocket (STOMP) + Kafka, persisted to PostgreSQL | [storyloom-community-service](https://github.com/ZahiqIbrahim/storyloom-community-service) |
| AI Recommendation Service | Gemini-powered book/movie recommendations, enriched via the Catalog Service | [storyloom-ai-recommendation-service](https://github.com/ZahiqIbrahim/storyloom-ai-recommendation-service) |
| Service Registry | Eureka server for service discovery | [storyloom-service-registry](https://github.com/ZahiqIbrahim/storyloom-service-registry) |
 
## Tech Stack
 
Java 21, Spring Boot, Spring Cloud (Eureka, Gateway, OpenFeign), Spring Security + JWT, Apache Kafka, WebSocket/STOMP, PostgreSQL, Docker, Google Gemini API.
 
## Running the Platform
 
Each service has its own setup instructions in its repo. At a high level:
 
1. Start the **Service Registry** (Eureka) first.
2. Start **Auth**, **Catalog**, **Community**, and **AI Recommendation** services — each registers with Eureka on startup.
3. Start the **API Gateway** last — it resolves all downstream services dynamically via Eureka.
All services can also be run together via Docker Compose on a shared network (see individual repos for service-specific environment variables).
 
## Video Demo
https://www.youtube.com/watch?v=M0lKUpwv4hU)
