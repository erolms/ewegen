
# Local Development Environment Setup

## Development Tools by Layer

### Frontend (React/Gatsby with TypeScript)

```bash
# Install NVM for Node version management
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash

# Install Node.js LTS
nvm install --lts
nvm use --lts

# Create Gatsby project with TypeScript and TailwindCSS
npm install -g gatsby-cli
gatsby new charity-frontend https://github.com/gatsbyjs/gatsby-starter-typescript
cd charity-frontend
npm install tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Testing frameworks
npm install --save-dev jest @testing-library/react @testing-library/jest-dom @testing-library/user-event jest-environment-jsdom msw
```

### BFF Layer (TypeScript/Node.js)

```bash
# Create TypeScript Node.js project
mkdir charity-bff
cd charity-bff
npm init -y
npm install --save express cors helmet winston aws-sdk

# TypeScript setup
npm install --save-dev typescript @types/node @types/express ts-node nodemon
npx tsc --init

# Testing frameworks
npm install --save-dev jest ts-jest @types/jest supertest @types/supertest
```

### Backend Services (Golang)

```bash
# Install Go
brew install go

# Initialize Go modules for each service
mkdir -p charity-services
cd charity-services
mkdir membership payments projects communications
cd membership
go mod init github.com/your-org/charity-system/membership
go get -u github.com/gin-gonic/gin
go get -u github.com/aws/aws-sdk-go-v2
go get -u github.com/stretchr/testify

# Initialize other services similarly
```

### Infrastructure

```bash
# Install AWS CLI and configure
brew install awscli
aws configure

# Install Docker and Docker Compose
brew install docker docker-compose

# Install LocalStack for local AWS services
docker pull localstack/localstack
```

## Folder Structure

```
charity-system/
├── frontend/                # Gatsby/React frontend
│   ├── src/
│   │   ├── components/      # Reusable UI components
│   │   ├── pages/           # Gatsby pages
│   │   ├── context/         # React context incl. auth
│   │   ├── hooks/           # Custom hooks
│   │   ├── services/        # API services
│   │   ├── utils/           # Utility functions
│   │   └── styles/          # Global styles
│   └── tests/               # Frontend tests
│
├── bff/                     # Backend for Frontend
│   ├── src/
│   │   ├── config/          # Configuration
│   │   ├── controllers/     # Route controllers
│   │   ├── middlewares/     # Express middlewares
│   │   ├── routes/          # API routes
│   │   ├── services/        # Business logic
│   │   ├── utils/           # Utilities
│   │   └── types/           # TypeScript types
│   └── tests/               # BFF tests
│
├── services/                # Golang microservices
│   ├── membership/          # Member management
│   ├── payments/            # Payment processing
│   ├── projects/            # Project management
│   └── communications/      # Email/notifications
│
├── shared/                  # Shared code
│   ├── auth/                # Auth library (TypeScript)
│   └── models/              # Shared data models
│
├── infrastructure/          # Infrastructure setup
│   ├── docker/              # Docker configuration
│   ├── aws/                 # AWS configuration
│   └── local/               # Local development
│
├── docs/                    # Documentation
│   ├── ADRs/                # Architecture Decision Records
│   └── api/                 # API documentation
│
└── scripts/                 # Development scripts
```

## Docker Compose Setup

```yaml
# docker-compose.yml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "8000:8000"
    volumes:
      - ./frontend:/app
      - /app/node_modules
    environment:
      - NODE_ENV=development

  bff:
    build: ./bff
    ports:
      - "3000:3000"
    volumes:
      - ./bff:/app
      - /app/node_modules
    environment:
      - NODE_ENV=development
    depends_on:
      - localstack

  membership:
    build: ./services/membership
    ports:
      - "8001:8001"
    volumes:
      - ./services/membership:/app
    environment:
      - APP_ENV=development
    depends_on:
      - localstack

  localstack:
    image: localstack/localstack
    ports:
      - "4566:4566"
    environment:
      - SERVICES=dynamodb,cognito,ses
    volumes:
      - ./infrastructure/local/init-aws.sh:/docker-entrypoint-initaws.d/init-aws.sh
```

## Key Choices Explained

### Frontend Testing Stack

- **Jest**: Industry standard for JavaScript testing
- **React Testing Library**: Encourages testing behavior over implementation
- **MSW (Mock Service Worker)**: API mocking that works with all requests
- **Cypress** (optional): For E2E testing with real browser rendering

**Pros**: Complete testing pyramid coverage, mock-free component testing
**Cons**: Initial setup complexity, multiple tools to learn

### Backend Testing Approach

- **Go**: Built-in testing package + testify for assertions
- **Node.js**: Jest for unit tests, Supertest for API testing

**Pros**: Standard tools with large community support
**Cons**: Different approaches per language stack

### Auth Development

- **LocalStack**: Simulates AWS services locally
- **Shared auth library**: Cross-platform consistency

**Pros**: Local development without AWS costs
**Cons**: Some divergence from actual AWS behavior

### DynamoDB Access

- **Local DynamoDB**: Via LocalStack
- **NoSQL Workbench**: For data modeling and visualization

**Pros**: Fast local development without cloud costs
**Cons**: Need to maintain schema consistency with production

## Getting Started

1. Set up the frontend:

```bash
cd frontend
npm install
npm run develop
```

2. Set up the BFF:

```bash
cd bff
npm install
npm run dev
```

3. Set up the Golang services:

```bash
cd services/membership
go mod download
go run main.go
```

4. Run the entire stack with Docker Compose:

```bash
docker-compose up
```

This setup facilitates TDD by providing isolated environments for each component while maintaining the ability to run the entire system locally. The folder structure supports clear separation of concerns while the shared authentication library ensures consistent implementation across components.
