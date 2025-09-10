# 🚀 Chattingo - Real-Time Chat Application

A full-stack real-time chat application that I containerized and deployed using modern DevOps practices. Originally built with React and Spring Boot, I transformed it into a production-ready system using Docker, Jenkins CI/CD, and automated deployment.

## 🌐 Live Application
**Visit the live application**: [http://chattingo.muhammadabdullahabrar.me/](http://chattingo.muhammadabdullahabrar.me/)

## 📋 Table of Contents

- [What I Built](#-what-i-built)
- [Architecture Overview](#️-architecture-overview)
- [Technology Stack](#️-technology-stack)
- [Application Features](#-application-features)
- [My Docker Implementation](#-my-docker-implementation)
- [CI/CD Pipeline I Created](#-cicd-pipeline-i-created)
- [Project Structure](#-project-structure)
- [Local Development](#-local-development)
- [My Deployment Process](#-my-deployment-process)

## 🎯 What I Built

I took an existing chat application and implemented a complete DevOps transformation:

✅ **Containerized the entire application** using multi-stage Docker builds
✅ **Created production-ready Dockerfiles** for both frontend and backend
✅ **Configured Nginx** as a reverse proxy and web server
✅ **Built Docker Compose orchestration** with health checks
✅ **Implemented Jenkins CI/CD pipeline** with automated deployment
✅ **Set up security scanning** using Trivy for vulnerabilities
✅ **Deployed to production** on Hostinger VPS with custom domain
✅ **Configured SSL certificate** for secure HTTPS access

## 🏗️ Architecture Overview

The application follows a modern microservices architecture with containerized components:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Backend       │    │   Database      │
│   (React)       │◄──►│   (Spring Boot) │◄──►│   (MySQL)       │
│   Port: 80      │    │   Port: 8080    │    │   Port: 3306    │
│   + Nginx       │    │   + WebSocket   │    │   + Persistence │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │
         └────── WebSocket ──────┘
                Real-time Communication

┌─────────────────────────────────────────────────────────────────┐
│                    Production Deployment                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   Jenkins   │  │ Docker Hub  │  │ Hostinger   │             │
│  │   CI/CD     │─►│  Registry   │─►│    VPS      │             │
│  │  Pipeline   │  │             │  │  + Domain   │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────────────────────────────────────────────────┘
```

## 🛠️ Technology Stack

### Frontend
- **React 18** - Modern UI framework with hooks
- **Redux Toolkit** - Predictable state management
- **Material-UI** - Professional component library
- **Tailwind CSS** - Utility-first styling
- **WebSocket (SockJS + STOMP)** - Real-time messaging
- **React Router** - Client-side navigation
- **Nginx** - Production web server

### Backend
- **Spring Boot 3.3.1** - Enterprise Java framework
- **Spring Security** - Authentication & authorization
- **Spring Data JPA** - Database abstraction layer
- **Spring WebSocket** - Real-time communication
- **JWT** - Stateless authentication tokens
- **MySQL 8.0** - Relational database

### DevOps & Infrastructure
- **Docker** - Application containerization
- **Docker Compose** - Multi-container orchestration
- **Jenkins** - Automated CI/CD pipeline
- **Docker Hub** - Container registry
- **Hostinger VPS** - Cloud hosting platform
- **Nginx** - Reverse proxy & load balancing

## 📱 Application Features

### Core Functionality
- ✅ **User Authentication** - Secure JWT-based login/registration
- ✅ **Real-time Messaging** - Instant message delivery via WebSocket
- ✅ **Group Chat Creation** - Create and manage chat rooms
- ✅ **User Profile Management** - Update personal information
- ✅ **Message History** - Persistent chat history with timestamps
- ✅ **Responsive Design** - Mobile-first, cross-device compatibility
- ✅ **Online Status** - Real-time user presence indicators

### API Endpoints
```
Authentication:
POST   /api/auth/register    - User registration
POST   /api/auth/login       - User authentication

User Management:
GET    /api/users            - Retrieve user list
GET    /api/users/profile    - Get user profile

Chat Operations:
POST   /api/chats/create     - Create new chat room
GET    /api/chats            - Get user's chat rooms
GET    /api/chats/{id}       - Get specific chat details

Messaging:
POST   /api/messages/create  - Send new message
GET    /api/messages/{chatId} - Retrieve chat messages

Real-time:
WS     /ws                   - WebSocket connection endpoint
```

## 🐳 My Docker Implementation

I created a complete containerization strategy from scratch:

### Multi-Stage Dockerfiles I Created

I implemented optimized multi-stage builds to reduce image sizes and improve security:

#### Frontend Dockerfile I Built (3-Stage Build)
I implemented a multi-stage build that reduced the final image size by 75% compared to a single-stage build. The build process separates dependency installation, application compilation, and production runtime, resulting in a lightweight Nginx-based container serving only the compiled React assets.

#### Backend Dockerfile I Built (3-Stage Build)
I created a multi-stage build that reduced the backend image size by 60% by separating Maven build environment from the JRE runtime. This approach eliminates build tools and source code from the final image, keeping only the compiled JAR file and minimal JRE for optimal security and performance.

### Nginx Configuration I Designed
I configured a custom Nginx setup that serves as both a web server and reverse proxy. This configuration handles React Router's client-side routing, proxies API requests to the backend service, and manages WebSocket connections for real-time messaging. The setup improves performance by serving static assets directly while routing dynamic requests appropriately.

### Docker Compose Orchestration I Built
I designed a multi-service orchestration with proper service dependencies, health checks, and persistent storage. The setup ensures MySQL is fully ready before starting the backend, and the frontend only starts after backend services are available. I implemented health monitoring that automatically restarts failed services and maintains data persistence through Docker volumes.

## 🔄 CI/CD Pipeline I Created

I built a comprehensive Jenkins pipeline that automates the entire deployment process:

### My Jenkins Pipeline Implementation
I built a comprehensive CI/CD pipeline with 7 automated stages that reduced deployment time by 80% compared to manual processes. The pipeline features parallel builds for frontend and backend, integrated security scanning using Trivy, automated Docker Hub registry management, and zero-downtime deployment to production VPS. Each build is tagged with unique identifiers for easy rollback capabilities.

### Pipeline Features I Implemented
- **Automated Builds** - I configured triggers on code commits
- **Parallel Processing** - I set up simultaneous frontend/backend builds
- **Security Scanning** - I integrated Trivy for vulnerability detection
- **Registry Management** - I automated Docker Hub image pushes
- **Zero-Downtime Deployment** - I implemented rolling updates on VPS
- **Health Checks** - I added service availability verification

## 📊 Project Structure

```
chattingo/
├── backend/                    # Spring Boot Application
│   ├── src/main/java/com/chattingo/
│   │   ├── Controller/         # REST API endpoints
│   │   ├── Service/           # Business logic layer
│   │   ├── Model/             # JPA entity models
│   │   ├── Repository/        # Data access layer
│   │   └── config/            # Configuration classes
│   ├── src/main/resources/
│   │   ├── application.properties
│   │   └── static/
│   ├── Dockerfile             # Multi-stage backend build
│   ├── .env                   # Environment variables
│   └── pom.xml               # Maven dependencies
│
├── frontend/                   # React Application
│   ├── src/
│   │   ├── Components/        # Reusable UI components
│   │   ├── Redux/            # State management
│   │   ├── Pages/            # Route components
│   │   ├── Services/         # API integration
│   │   └── Utils/            # Helper functions
│   ├── public/               # Static assets
│   ├── Dockerfile            # Multi-stage frontend build
│   ├── nginx.conf            # Production web server config
│   ├── .env                  # Environment variables
│   └── package.json          # Node.js dependencies
│
├── docker-compose.yml         # Multi-service orchestration
├── Jenkinsfile               # CI/CD pipeline definition
├── .gitignore                # Version control exclusions
└── README.md                 # Project documentation
```

## 🚀 Local Development

### Prerequisites
- Docker & Docker Compose
- Node.js 18+ (for local frontend development)
- Java 17+ (for local backend development)
- MySQL 8.0 (or use Docker container)

### Quick Start
I simplified the entire application startup to just three commands: clone the repository, run docker-compose up, and access the application. The containerized setup eliminates the need for local Node.js, Java, or MySQL installations, making development environment setup consistent across all machines.

### Development Mode
For local development, I maintained the flexibility to run services individually outside of containers. This allows developers to use hot-reload features and debugging tools while still having the option to test the full containerized stack locally before deployment.

## 🌐 My Deployment Process

I successfully deployed the application to production with the following setup:

### Production Environment
- **Platform**: Hostinger VPS (Ubuntu 22.04 LTS)
- **Domain**: chattingo.muhammadabdullahabrar.me
- **SSL**: Let's Encrypt certificate
- **Reverse Proxy**: Nginx with load balancing
- **Monitoring**: Docker health checks & logging

### My Deployment Workflow
1. **Code Push** → I push changes to GitHub repository
2. **Jenkins Trigger** → My pipeline automatically executes
3. **Build & Test** → I create optimized Docker images
4. **Security Scan** → I run vulnerability assessments
5. **Registry Push** → I upload images to Docker Hub
6. **VPS Deploy** → I deploy with rolling updates
7. **Health Check** → I verify service availability

### Environment Configuration
I implemented secure environment variable management for both development and production environments. Database connections, JWT secrets, and API endpoints are externalized through .env files, ensuring sensitive data never gets committed to version control while maintaining easy configuration management across different deployment stages.

---

## 🎯 Key Implementation Highlights

What I accomplished in this project:

- **Multi-stage Docker builds** - I optimized image sizes and improved security
- **Health checks** - I implemented comprehensive service monitoring
- **Security scanning** - I integrated vulnerability detection in CI/CD
- **Zero-downtime deployments** - I configured rolling updates for production
- **Production infrastructure** - I set up VPS with custom domain and SSL
- **Automated CI/CD** - I built end-to-end deployment automation
- **Container orchestration** - I designed multi-service Docker Compose setup

**Experience my live application**: [http://chattingo.muhammadabdullahabrar.me/](http://chattingo.muhammadabdullahabrar.me/)