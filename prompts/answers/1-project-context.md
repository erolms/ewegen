
# Charity Management System Knowledge Base

## Core Architecture

* Three-tier application: React/Gatsby frontend with TailwindCSS, TypeScript BFF, Golang microservices
* Database: DynamoDB document-based persistence
* AWS Services: Cognito (auth), SES (email)

## Key Features

* Membership data management
* Recurring payment processing (internal)
* Project fulfillment tracking
* Email communication
* GDPR compliance (30-day archive, 10-year retention)

## Technical Requirements

* Modular, extensible codebase
* Containerized backend (rootless Docker)
* Accessible, responsive, internationalized frontend
* Offline capability with synchronization
* RESTful APIs with proper error handling
* Observability (logging, monitoring, metrics)

## Development Standards

* Test-driven development with comprehensive test coverage
* Decoupled architecture for component interchangeability
* Inline documentation with OpenAPI v3 specs
* Security-first approach with CI scanning
* Trunk-based development with semantic versioning
* Continuous delivery and pair programming reviews

## Additional Recommendations

* Dependency management and versioning strategy
* Disaster recovery and backup procedures
* Environment configuration management
* Performance testing and optimization guidelines
* Onboarding process for new developers
* Browser/device compatibility requirements
* Technical debt management approach
* System monitoring alert thresholds