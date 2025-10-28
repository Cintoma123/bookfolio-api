# 📚 Advanced Book Management System

[![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=for-the-badge&logo=nestjs&logoColor=white)](https://nestjs.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)

A production-ready, enterprise-grade book management platform featuring AI-powered recommendations, real-time collaboration, multi-tenant architecture, and advanced search capabilities. Built with modern DevOps practices and cloud-native architecture.

---

## 📘 Overview

The Advanced Book Management System is a comprehensive solution for libraries, educational institutions, and organizations to manage their book collections efficiently. It combines traditional CRUD operations with cutting-edge AI features, real-time collaboration tools, and intelligent search capabilities.

### Key Features

- 🤖 **AI-Powered Assistant** - LangChain integration with RAG for intelligent book recommendations and queries
- 🏢 **Multi-Tenant Architecture** - Complete isolation between organizations with shared infrastructure
- 💬 **Real-Time Chat** - WebSocket-based communication for collaborative reading groups and discussions
- 🔍 **Advanced Search** - ElasticSearch integration for lightning-fast, fuzzy search across millions of books
- 🔐 **Enterprise Authentication** - JWT-based auth with role-based access control (RBAC)
- 📊 **Analytics Dashboard** - Real-time insights into reading patterns and book popularity
- 🚀 **Microservices Ready** - Modular architecture prepared for horizontal scaling
- 🐳 **Containerized Deployment** - Full Docker support with orchestration-ready configuration
- 📈 **Observability** - Integrated monitoring, logging, and alerting with Prometheus & Grafana

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         Client Layer                             │
│  (Web App, Mobile App, Third-party Integrations)                │
└────────────────┬────────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────────┐
│                     API Gateway / Load Balancer                  │
│                    (NGINX / AWS ALB)                            │
└────────────────┬────────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────────┐
│                      NestJS Application                          │
│  ┌──────────────┬──────────────┬──────────────┬──────────────┐ │
│  │   Auth       │   Books      │   AI Chat    │   Search     │ │
│  │   Module     │   Module     │   Module     │   Module     │ │
│  └──────────────┴──────────────┴──────────────┴──────────────┘ │
│  ┌──────────────┬──────────────┬──────────────┬──────────────┐ │
│  │   Users      │   Tenants    │   Analytics  │   WebSocket  │ │
│  │   Module     │   Module     │   Module     │   Gateway    │ │
│  └──────────────┴──────────────┴──────────────┴──────────────┘ │
└────────────────┬────────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────────┐
│                      Data & Services Layer                       │
│  ┌──────────────┬──────────────┬──────────────┬──────────────┐ │
│  │  PostgreSQL  │ ElasticSearch│    Redis     │   AWS S3     │ │
│  │  (Primary)   │  (Search)    │   (Cache)    │  (Storage)   │ │
│  └──────────────┴──────────────┴──────────────┴──────────────┘ │
│  ┌──────────────┬──────────────┬──────────────┬──────────────┐ │
│  │  LangChain   │  Vector DB   │  Prometheus  │   Grafana    │ │
│  │  (AI/RAG)    │  (Pinecone)  │ (Metrics)    │ (Monitoring) │ │
│  └──────────────┴──────────────┴──────────────┴──────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

### Request Flow

1. **Client Request** → API Gateway (authentication, rate limiting)
2. **API Gateway** → NestJS Application (routing, validation)
3. **NestJS Guards** → Validate JWT, check tenant context, verify permissions
4. **Business Logic** → Process request through appropriate module
5. **Data Layer** → Query PostgreSQL, ElasticSearch, or Redis as needed
6. **AI Processing** (if needed) → LangChain + Vector DB for recommendations
7. **Response** → Transform and return data to client

---

## 📂 Project Structure

```
book-management-system/
├── src/
│   ├── modules/
│   │   ├── auth/
│   │   │   ├── auth.controller.ts
│   │   │   ├── auth.service.ts
│   │   │   ├── auth.module.ts
│   │   │   ├── strategies/
│   │   │   │   ├── jwt.strategy.ts
│   │   │   │   └── local.strategy.ts
│   │   │   └── guards/
│   │   │       ├── jwt-auth.guard.ts
│   │   │       └── roles.guard.ts
│   │   ├── books/
│   │   │   ├── books.controller.ts
│   │   │   ├── books.service.ts
│   │   │   ├── books.module.ts
│   │   │   ├── entities/
│   │   │   │   └── book.entity.ts
│   │   │   └── dto/
│   │   │       ├── create-book.dto.ts
│   │   │       └── update-book.dto.ts
│   │   ├── ai-assistant/
│   │   │   ├── ai-assistant.controller.ts
│   │   │   ├── ai-assistant.service.ts
│   │   │   ├── ai-assistant.module.ts
│   │   │   └── langchain/
│   │   │       ├── rag.service.ts
│   │   │       └── embeddings.service.ts
│   │   ├── search/
│   │   │   ├── search.controller.ts
│   │   │   ├── search.service.ts
│   │   │   └── elasticsearch.config.ts
│   │   ├── chat/
│   │   │   ├── chat.gateway.ts
│   │   │   ├── chat.service.ts
│   │   │   └── chat.module.ts
│   │   ├── tenants/
│   │   │   ├── tenants.controller.ts
│   │   │   ├── tenants.service.ts
│   │   │   ├── tenants.module.ts
│   │   │   └── tenant.middleware.ts
│   │   ├── users/
│   │   │   ├── users.controller.ts
│   │   │   ├── users.service.ts
│   │   │   └── users.module.ts
│   │   └── analytics/
│   │       ├── analytics.controller.ts
│   │       ├── analytics.service.ts
│   │       └── analytics.module.ts
│   ├── common/
│   │   ├── decorators/
│   │   │   ├── roles.decorator.ts
│   │   │   └── tenant.decorator.ts
│   │   ├── filters/
│   │   │   └── http-exception.filter.ts
│   │   ├── interceptors/
│   │   │   ├── logging.interceptor.ts
│   │   │   └── transform.interceptor.ts
│   │   ├── pipes/
│   │   │   └── validation.pipe.ts
│   │   └── interfaces/
│   │       └── tenant.interface.ts
│   ├── config/
│   │   ├── database.config.ts
│   │   ├── redis.config.ts
│   │   ├── elasticsearch.config.ts
│   │   └── aws.config.ts
│   ├── database/
│   │   ├── migrations/
│   │   └── seeds/
│   ├── app.module.ts
│   └── main.ts
├── test/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── docker/
│   ├── Dockerfile
│   ├── Dockerfile.prod
│   └── docker-compose.yml
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── configmap.yaml
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── cd.yml
├── docs/
│   ├── api/
│   ├── architecture/
│   └── deployment/
├── scripts/
│   ├── setup.sh
│   ├── migrate.sh
│   └── seed.sh
├── .env.example
├── .gitignore
├── nest-cli.json
├── package.json
├── tsconfig.json
├── README.md
└── LICENSE
```

---

## ⚙️ Tech Stack

### Core Framework
- **NestJS** (v10.x) - Progressive Node.js framework
- **TypeScript** (v5.x) - Type-safe JavaScript
- **Node.js** (v20.x LTS) - Runtime environment

### Database & ORM
- **PostgreSQL** (v15.x) - Primary relational database
- **TypeORM** (v0.3.x) - Object-relational mapping
- **Redis** (v7.x) - Caching and session management

### Search & Analytics
- **ElasticSearch** (v8.x) - Full-text search engine
- **Kibana** (v8.x) - Search analytics visualization

### AI & Machine Learning
- **LangChain** (v0.1.x) - AI orchestration framework
- **OpenAI API** - GPT models for natural language processing
- **Pinecone** - Vector database for embeddings
- **FAISS** - Alternative vector similarity search

### Real-Time Communication
- **Socket.io** (v4.x) - WebSocket communication
- **@nestjs/websockets** - NestJS WebSocket adapter

### Authentication & Security
- **Passport.js** - Authentication middleware
- **JWT** - JSON Web Tokens
- **bcrypt** - Password hashing
- **Helmet** - Security headers
- **rate-limiter-flexible** - Rate limiting

### Cloud & Infrastructure
- **AWS ECS** - Container orchestration
- **AWS RDS** - Managed PostgreSQL
- **AWS S3** - Object storage for book covers/files
- **AWS CloudFront** - CDN for static assets
- **AWS ElastiCache** - Managed Redis

### DevOps & Monitoring
- **Docker** & **Docker Compose** - Containerization
- **GitHub Actions** - CI/CD pipelines
- **Terraform** - Infrastructure as Code
- **Prometheus** - Metrics collection
- **Grafana** - Metrics visualization
- **Winston** - Application logging
- **Sentry** - Error tracking

### Testing
- **Jest** - Unit and integration testing
- **Supertest** - API endpoint testing
- **@faker-js/faker** - Test data generation

### Documentation
- **Swagger/OpenAPI** - API documentation
- **Compodoc** - Code documentation generator

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** v20.x or higher
- **Docker** & **Docker Compose** v24.x or higher
- **PostgreSQL** v15.x (if running locally without Docker)
- **Redis** v7.x (if running locally without Docker)
- **ElasticSearch** v8.x (if running locally without Docker)
- **AWS Account** (for deployment)
- **OpenAI API Key** (for AI features)

### Environment Variables

Create a `.env` file in the root directory:

```env
# Application
NODE_ENV=development
PORT=3000
API_PREFIX=api/v1

# Database
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USER=bookadmin
DATABASE_PASSWORD=your_secure_password
DATABASE_NAME=book_management
DATABASE_SSL=false

# JWT
JWT_SECRET=your_super_secret_jwt_key_change_in_production
JWT_EXPIRATION=7d
JWT_REFRESH_SECRET=your_refresh_token_secret
JWT_REFRESH_EXPIRATION=30d

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=
REDIS_TTL=3600

# ElasticSearch
ELASTICSEARCH_NODE=http://localhost:9200
ELASTICSEARCH_USERNAME=elastic
ELASTICSEARCH_PASSWORD=changeme
ELASTICSEARCH_INDEX=books

# AI Configuration
OPENAI_API_KEY=sk-your-openai-api-key
PINECONE_API_KEY=your-pinecone-api-key
PINECONE_ENVIRONMENT=us-west1-gcp
PINECONE_INDEX=book-embeddings

# AWS Configuration
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_S3_BUCKET=book-management-assets

# Monitoring
SENTRY_DSN=https://your-sentry-dsn@sentry.io/project-id
PROMETHEUS_PORT=9090

# CORS
CORS_ORIGIN=http://localhost:3000,http://localhost:4200

# Rate Limiting
RATE_LIMIT_TTL=60
RATE_LIMIT_MAX=100
```

### Local Development Setup

#### Option 1: Using Docker (Recommended)

```bash
# Clone the repository
git clone https://github.com/your-org/book-management-system.git
cd book-management-system

# Copy environment variables
cp .env.example .env

# Edit .env with your configuration
nano .env

# Start all services with Docker Compose
docker-compose up -d

# Run database migrations
npm run migration:run

# Seed initial data
npm run seed

# Application will be available at http://localhost:3000
# Swagger documentation at http://localhost:3000/api/docs
```

#### Option 2: Manual Setup

```bash
# Clone the repository
git clone https://github.com/your-org/book-management-system.git
cd book-management-system

# Install dependencies
npm install

# Setup PostgreSQL database
createdb book_management

# Setup and start Redis
redis-server

# Setup and start ElasticSearch
# Download from https://www.elastic.co/downloads/elasticsearch
elasticsearch

# Copy environment variables
cp .env.example .env

# Edit .env with your local configuration
nano .env

# Run database migrations
npm run migration:run

# Seed initial data
npm run seed

# Start development server
npm run start:dev

# Application will be available at http://localhost:3000
```

### Docker Compose Services

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f app

# Stop all services
docker-compose down

# Rebuild and start
docker-compose up -d --build

# Scale specific service
docker-compose up -d --scale app=3
```

### Available Scripts

```bash
# Development
npm run start:dev        # Start with hot-reload
npm run start:debug      # Start with debugging

# Production
npm run build            # Build for production
npm run start:prod       # Run production build

# Database
npm run migration:create # Create new migration
npm run migration:run    # Run migrations
npm run migration:revert # Revert last migration
npm run seed             # Seed database

# Testing
npm run test             # Run unit tests
npm run test:watch       # Run tests in watch mode
npm run test:cov         # Generate coverage report
npm run test:e2e         # Run end-to-end tests

# Linting & Formatting
npm run lint             # Run ESLint
npm run format           # Format with Prettier

# Documentation
npm run doc              # Generate documentation
```

---

## 🔒 Authentication & Authorization

### Authentication Flow

1. **Registration** - User creates account with email/password
2. **Email Verification** - Verification link sent to email
3. **Login** - Credentials validated, JWT tokens issued
4. **Access Token** - Short-lived token (7 days) for API requests
5. **Refresh Token** - Long-lived token (30 days) to obtain new access tokens

### Role-Based Access Control (RBAC)

| Role | Permissions |
|------|-------------|
| **Super Admin** | Full system access, manage tenants, global configuration |
| **Tenant Admin** | Manage organization, users, books, settings within tenant |
| **Librarian** | CRUD operations on books, manage borrowing, generate reports |
| **Member** | View books, borrow/return, participate in chat, use AI assistant |
| **Guest** | Read-only access to public books, limited search |

### API Authentication

```typescript
// Example: Protected endpoint
@UseGuards(JwtAuthGuard, RolesGuard)
@Roles('admin', 'librarian')
@Get('books/:id')
async getBook(@Param('id') id: string) {
  return this.booksService.findOne(id);
}

// Example: Tenant-scoped endpoint
@UseGuards(JwtAuthGuard, TenantGuard)
@Get('tenant/books')
async getTenantBooks(@TenantId() tenantId: string) {
  return this.booksService.findByTenant(tenantId);
}
```

### Request Headers

```bash
# Authentication
Authorization: Bearer <jwt_token>

# Tenant Context
X-Tenant-ID: <tenant_uuid>

# API Version
Accept: application/json; version=1
```

---

## 🧠 AI Assistant Features

### LangChain Integration

The AI Assistant uses LangChain to provide intelligent book recommendations and answer natural language queries about books in the system.

#### Key Capabilities

1. **Semantic Search** - Natural language book queries
2. **Personalized Recommendations** - Based on reading history and preferences
3. **Question Answering** - Ask questions about book content, authors, themes
4. **Summarization** - Generate book summaries and reviews
5. **Genre Classification** - Automatic genre tagging using ML

### RAG (Retrieval-Augmented Generation) Architecture

```
User Query → Embedding Model → Vector Search (Pinecone)
              ↓
         Top K Results → LangChain → GPT-4 → Contextual Response
              ↓
      Book Metadata (PostgreSQL)
```

### AI Endpoints

```bash
# Ask question about books
POST /api/v1/ai/query
{
  "query": "Recommend science fiction books about space exploration",
  "context": "user_preferences",
  "maxResults": 5
}

# Generate book summary
POST /api/v1/ai/summarize
{
  "bookId": "uuid",
  "length": "short" | "medium" | "long"
}

# Get personalized recommendations
GET /api/v1/ai/recommendations?userId=uuid&count=10
```

### Configuration

```typescript
// AI Assistant Configuration
export const aiConfig = {
  model: 'gpt-4-turbo',
  temperature: 0.7,
  maxTokens: 1000,
  embeddingModel: 'text-embedding-ada-002',
  vectorDimensions: 1536,
  topK: 5,
  similarityThreshold: 0.75
};
```

---

## 🏢 Multi-Tenant Architecture

### Tenant Isolation Strategies

1. **Database-Level** - Separate schema per tenant
2. **Row-Level** - Shared tables with `tenant_id` column
3. **Hybrid Approach** - Critical data isolated, shared tables for common data

### Tenant Context Flow

```typescript
// Middleware extracts tenant from JWT or header
@Injectable()
export class TenantMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    const tenantId = req.headers['x-tenant-id'] || req.user?.tenantId;
    req['tenantId'] = tenantId;
    next();
  }
}

// Services automatically scope queries
@Injectable()
export class BooksService {
  async findAll(tenantId: string) {
    return this.bookRepository.find({ where: { tenantId } });
  }
}
```

### Tenant Management

```bash
# Create new tenant
POST /api/v1/tenants
{
  "name": "Acme Library System",
  "domain": "acme.bookmanagement.io",
  "plan": "enterprise",
  "settings": {
    "maxUsers": 500,
    "maxBooks": 50000
  }
}

# Tenant-specific configuration
GET /api/v1/tenants/:id/config
PUT /api/v1/tenants/:id/config
```

---

## 💬 Real-Time Chat System

### WebSocket Architecture

```typescript
// Chat Gateway
@WebSocketGateway({
  cors: { origin: '*' },
  namespace: '/chat'
})
export class ChatGateway {
  @SubscribeMessage('joinRoom')
  handleJoinRoom(client: Socket, roomId: string) {
    client.join(roomId);
    return { event: 'joinedRoom', data: roomId };
  }

  @SubscribeMessage('sendMessage')
  handleMessage(client: Socket, payload: MessageDto) {
    this.server.to(payload.roomId).emit('newMessage', payload);
  }
}
```

### Chat Features

- **Reading Groups** - Create book discussion rooms
- **Direct Messaging** - One-on-one user communication
- **Presence Tracking** - Online/offline status
- **Message History** - Persistent message storage
- **File Sharing** - Share book notes and annotations
- **Typing Indicators** - Real-time typing status

### Client Connection

```javascript
// Connect to WebSocket
const socket = io('http://localhost:3000/chat', {
  auth: { token: jwt_token },
  query: { tenantId: tenant_id }
});

// Join a reading group
socket.emit('joinRoom', 'book-club-sci-fi');

// Send message
socket.emit('sendMessage', {
  roomId: 'book-club-sci-fi',
  message: 'Great book!',
  userId: 'user-uuid'
});

// Listen for new messages
socket.on('newMessage', (message) => {
  console.log('New message:', message);
});
```

---

## 🔍 ElasticSearch Integration

### Search Capabilities

- **Full-Text Search** - Search across title, author, description, ISBN
- **Fuzzy Matching** - Handle typos and spelling variations
- **Faceted Search** - Filter by genre, author, year, rating
- **Autocomplete** - Real-time search suggestions
- **Relevance Scoring** - Intelligent result ranking
- **Geo-Search** - Find books available in nearby libraries

### Index Configuration

```typescript
// Book Index Mapping
const bookIndexMapping = {
  properties: {
    title: { type: 'text', analyzer: 'english' },
    author: { type: 'text', analyzer: 'standard' },
    isbn: { type: 'keyword' },
    description: { type: 'text', analyzer: 'english' },
    genre: { type: 'keyword' },
    publishYear: { type: 'integer' },
    rating: { type: 'float' },
    location: { type: 'geo_point' },
    tenantId: { type: 'keyword' }
  }
};
```

### Search API Examples

```bash
# Basic search
GET /api/v1/search?q=harry+potter

# Advanced search with filters
GET /api/v1/search?q=science+fiction&genre=scifi&year=2020-2024&minRating=4.0

# Autocomplete
GET /api/v1/search/autocomplete?q=harr

# Geo-search (books within 10km)
GET /api/v1/search/nearby?lat=40.7128&lon=-74.0060&distance=10km
```

---

## 🧩 Modular Architecture

### Module Organization

Each feature is encapsulated in its own module with clear boundaries:

- **Auth Module** - Authentication, authorization, JWT management
- **Books Module** - CRUD operations, borrowing, ratings
- **Users Module** - User management, profiles, preferences
- **Tenants Module** - Multi-tenancy, organization management
- **AI Assistant Module** - LangChain, RAG, recommendations
- **Search Module** - ElasticSearch integration, indexing
- **Chat Module** - WebSocket, real-time messaging
- **Analytics Module** - Reporting, dashboards, metrics

### Microservices Preparation

The modular structure allows easy transition to microservices:

```yaml
# Example: Extracting AI Assistant to separate service
services:
  api-gateway:
    image: book-management-api-gateway
    ports: ["3000:3000"]
  
  books-service:
    image: book-management-books
    ports: ["3001:3001"]
  
  ai-service:
    image: book-management-ai
    ports: ["3002:3002"]
    environment:
      - OPENAI_API_KEY=${OPENAI_API_KEY}
  
  search-service:
    image: book-management-search
    ports: ["3003:3003"]
```

---

## 🧑‍💻 DevOps & CI/CD

### GitHub Actions Pipeline

```yaml
# .github/workflows/ci.yml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '20'
      - run: npm ci
      - run: npm run lint
      - run: npm run test:cov
      - run: npm run test:e2e

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: |
            ${{ secrets.ECR_REGISTRY }}/book-management:latest
            ${{ secrets.ECR_REGISTRY }}/book-management:${{ github.sha }}

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy to AWS ECS
        run: |
          aws ecs update-service \
            --cluster book-management-prod \
            --service book-management-api \
            --force-new-deployment
```

### Docker Configuration

```dockerfile
# Production Dockerfile
FROM node:20-alpine AS builder

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force
COPY . .
RUN npm run build

FROM node:20-alpine AS production

WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./

EXPOSE 3000
CMD ["node", "dist/main.js"]
```

### Monitoring Stack

**Prometheus Metrics**
- Request latency and throughput
- Database query performance
- Cache hit/miss rates
- Active WebSocket connections
- AI model inference times

**Grafana Dashboards**
- Application health overview
- API performance metrics
- Database connection pools
- ElasticSearch cluster health
- Business metrics (books added, users registered, etc.)

**Sentry Error Tracking**
- Real-time error reporting
- Stack traces and context
- User session replay
- Performance monitoring

### Health Checks

```typescript
// Health check endpoints
@Get('health')
healthCheck() {
  return {
    status: 'ok',
    timestamp: new Date().toISOString(),
    uptime: process.uptime(),
    database: 'connected',
    redis: 'connected',
    elasticsearch: 'connected'
  };
}

@Get('metrics')
metrics() {
  // Prometheus-formatted metrics
}
```

---

## 🧾 API Documentation

### Swagger/OpenAPI

Interactive API documentation is available at `/api/docs` when running the application.

**Key Endpoint Groups:**

- **Authentication** - `/api/v1/auth/*`
- **Books** - `/api/v1/books/*`
- **Users** - `/api/v1/users/*`
- **Search** - `/api/v1/search/*`
- **AI Assistant** - `/api/v1/ai/*`
- **Analytics** - `/api/v1/analytics/*`
- **Tenants** - `/api/v1/tenants/*`

### Postman Collection

Import the Postman collection from `/docs/api/postman-collection.json` for quick API testing.

```bash
# Generate Postman collection
npm run postman:generate
```

### API Versioning

The API supports versioning through URL paths:

```
/api/v1/books  # Version 1
/api/v2/books  # Version 2 (future)
```

### Rate Limiting

```
Rate Limit: 100 requests per minute per user
Headers:
  X-RateLimit-Limit: 100
  X-RateLimit-Remaining: 87
  X-RateLimit-Reset: 1699564800
```

---

## 🌍 AWS Deployment Architecture

### Infrastructure Overview

```
┌─────────────────────────────────────────────────────┐
│                    Route 53 (DNS)                    │
└──────────────────────┬──────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────┐
│              CloudFront (CDN)                        │
└──────────────────────┬──────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────┐
│    Application Load Balancer (ALB)                  │
└──────────────────────┬──────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────┐
│              ECS Fargate Cluster                     │
│  ┌──────────────┬──────────────┬──────────────┐    │
│  │  API Task 1  │  API Task 2  │  API Task 3