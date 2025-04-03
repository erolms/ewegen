# eWegen - Ehrenamtswegen - Mitglieder Management Plattform

A comprehensive management system for volunteer-run charity organizations.

## Project Summary

The eWegen platform (Ehrenamtswegen - Mitglieder Management Plattform) is a three-tier application designed to help volunteers efficiently manage their charity organization's operations. It provides tools for membership management, payment processing, project fulfillment tracking, and member communications while ensuring GDPR compliance.

The system is built with a focus on usability, accessibility, and offline capability to support volunteers working in diverse environments. It leverages modern web technologies with React/Gatsby on the frontend, a TypeScript BFF (Backend for Frontend) layer, and Golang microservices for core functionality.

## Project Goals

- Simplify membership data management for volunteer-run charities
- Provide reliable tools for tracking recurring payments and financial data
- Enable efficient project fulfillment tracking and management
- Facilitate communication with members through email and notifications
- Ensure GDPR compliance and proper data retention
- Support offline usage with synchronization capabilities
- Create an accessible, internationalized user interface
- Deliver a system that is easy to maintain and extend

## Context

Volunteer-run charity organizations often struggle with administrative tasks due to limited resources, technical expertise, and inconsistent access to technology. Many rely on spreadsheets, paper records, or fragmented software solutions that don't meet their specific needs.

eWegen aims to address these challenges by providing a unified, purpose-built system that is both powerful and accessible to users with varying technical skills. By streamlining administrative tasks, the system allows volunteers to focus more on their core mission of helping others.

## Problem Statement

We need a technical solution that enables:

- Efficient management of membership data and recurring payments
- Fulfillment tracking of support projects
- Secure member communication
- GDPR compliance and proper data retention
- Scalability and extensibility for future requirements
- Easy maintenance by volunteer staff with varying technical expertise
- Offline capabilities to accommodate volunteers working in various conditions
- Comprehensive documentation to support onboarding of new volunteers

## Architecture

The system follows a three-tier architecture with domain-specific microservices:

1. **Frontend**: Static TypeScript application using React/Gatsby with TailwindCSS
2. **Backend for Frontend (BFF)**: TypeScript with Node.js runtime
3. **Domain-Specific Backend Services**: Golang microservices for optimal performance

Key architectural components include:

- AWS Cognito for authentication/authorization
- DynamoDB for data persistence
- AWS SES for email communications
- Docker containers for service deployment

For detailed architectural decisions, please refer to our Architecture Decision Records:

- [ADR0001: Core Architecture](docs/ADRs/ADR0001-project-adr.md)
- [ADR0002: Authentication/Authorization Architecture](docs/ADRs/ADR0002-auth-architecture.md)

Our [Project Roadmap](prompts/answers/3-project-roadmap.md) outlines the development phases and timeline.

## Setup Instructions

### Prerequisites

- Node.js (LTS version)
- Go 1.19+
- Docker and Docker Compose
- AWS CLI (for production deployment)

### Quick Start

1. Clone the repository with submodules:

```bash
git clone --recurse-submodules https://github.com/erolms/ewegen.git
cd ewegen
```

2. Start the development environment:

```bash
docker-compose up
```

3. Access the applications:

   - Frontend: [http://localhost:8000](http://localhost:8000)
   - BFF API: [http://localhost:3000](http://localhost:3000)
   - API Documentation: [http://localhost:3000/api-docs](http://localhost:3000/api-docs)

For detailed setup instructions, see [Local Environment Setup](prompts/answers/6-local-env-setup.md)

## Contributing

We welcome contributions to eWegen! Please review our [Contribution Guidelines](CONTRIBUTING.md) before getting started.

### Git Submodules

This project uses Git submodules to manage shared components. When cloning the repository, always use:

```bash
git clone --recurse-submodules https://github.com/erolms/ewegen.git
```

If you've already cloned the repository without submodules, initialize them with:

```bash
git submodule update --init --recursive
```

When updating submodules:

```bash
git submodule update --remote
```

### Development Workflow

1. Create a feature branch from `main`
2. Implement your changes with tests
3. Ensure all tests pass
4. Submit a pull request

We follow test-driven development practices. Please ensure all code has appropriate test coverage.

## Authors

- [Eeol Zavidic](https://github.com/erolms) - Initial work and architecture

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Thanks to all the volunteers who provided requirements and feedback
- All open source project contributors whose libraries made this project possible
