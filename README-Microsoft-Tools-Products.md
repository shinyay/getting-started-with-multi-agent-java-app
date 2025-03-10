# Microsoft Tools and Products Used in this Project

This document provides detailed explanations of all the Microsoft tools and products used in the Multi-Agent Banking Assistant application.

## Programming Languages and Frameworks

### Java
Java serves as the primary backend language for this project. It provides platform independence, strong typing, and extensive libraries which make it ideal for enterprise applications. In this project, Java powers all the backend microservices including the account, payment, transaction history, and copilot services.

### Spring Boot
Spring Boot is an open-source Java-based framework that simplifies the development of standalone, production-grade Spring-based applications. In this project, Spring Boot provides:
- Auto-configuration of application components
- Embedded server capabilities
- Health monitoring and metrics
- Simplified dependency management
- RESTful API development capabilities for our microservices

### TypeScript
TypeScript is a strongly-typed superset of JavaScript that adds static types to the language. In this project, TypeScript powers the frontend application, providing better tooling, earlier detection of errors, and improved developer experience through features like autocompletion and interface definitions.

### React
React is a JavaScript library for building user interfaces, particularly single-page applications. In this project, React is used to build the frontend application, providing:
- Component-based architecture for reusable UI elements
- Virtual DOM for efficient rendering
- Declarative approach to UI development
- Integration with TypeScript for type safety

## AI and Cognitive Services

### Azure OpenAI
Azure OpenAI provides REST API access to OpenAI's powerful language models including GPT-4. In this project, Azure OpenAI serves as the foundation for the multi-agent system by:
- Powering natural language understanding and generation
- Enabling the Router Agent to analyze user intent
- Allowing specialist agents to generate human-like responses
- Supporting semantic functions in the Semantic Kernel framework

### Azure Document Intelligence (formerly Form Recognizer)
Azure Document Intelligence is an AI service that extracts text, key-value pairs, tables, and structure from documents. In this project, it's used by the Payment Agent to:
- Process uploaded invoice images
- Extract relevant payment information like amounts, due dates, and payee details
- Convert unstructured document data into structured information that can be processed by the payment service

## Semantic Kernel

Semantic Kernel is an open-source framework that integrates AI services like Azure OpenAI with conventional programming languages. In this project, it serves as the orchestration layer that:
- Enables the creation and management of AI agents
- Connects natural language capabilities with programming primitives
- Provides a plugin system for extending AI capabilities with traditional code
- Manages context and memory for conversational interactions
- Implements the OpenAPI plugin for connecting to business microservices

## Containerization and Orchestration

### Docker
Docker is a platform that uses OS-level virtualization to deliver software in packages called containers. In this project, Docker is used to:
- Package each microservice and the frontend into isolated containers
- Ensure consistency across development, testing, and production environments
- Simplify dependency management
- Enable portable deployments across different environments

### Docker Compose
Docker Compose is a tool for defining and running multi-container Docker applications. In this project, it's used for:
- Local development environment setup
- Orchestrating the startup of all services in the correct order
- Managing service dependencies and networking
- Providing a consistent developer experience across different platforms

### Azure Container Apps
Azure Container Apps is a fully managed serverless container service for building and deploying modern applications at scale. In this project, it:
- Hosts all containerized services (frontend, copilot, account, payment, transaction)
- Provides built-in autoscaling capabilities
- Manages service-to-service communication
- Handles HTTPS termination and routing
- Integrates with Azure monitoring services

### Kubernetes (for deployment manifests)
While the primary deployment target is Azure Container Apps, the project includes Kubernetes manifests for:
- Alternative deployment options on Azure Kubernetes Service (AKS)
- Standardized deployment specifications
- Declarative configuration of application services
- Resource management (CPU, memory)

## Infrastructure as Code

### Bicep
Bicep is a domain-specific language (DSL) for deploying Azure resources declaratively. In this project, Bicep is used to:
- Define all Azure resources required by the application
- Ensure repeatable and consistent deployments
- Manage resource dependencies and relationships
- Parameterize deployments for different environments
- Organize infrastructure into modular components

## Build and Dependency Management

### Maven
Maven is a build automation tool used primarily for Java projects. In this project, Maven:
- Manages dependencies for all Java services
- Defines build lifecycles and processes
- Generates project documentation
- Facilitates testing and packaging
- Creates Docker-compatible artifacts

### NPM (Node Package Manager)
NPM is the package manager for JavaScript/TypeScript projects. In this project, NPM is used to:
- Manage frontend dependencies
- Run development scripts and commands
- Define build processes for the React application
- Manage TypeScript compilation
- Handle asset optimization

## Continuous Integration and Deployment

### GitHub Actions
GitHub Actions is a CI/CD platform that automates software workflows. In this project, it's used to:
- Automatically build and test code on pull requests
- Deploy infrastructure and applications to Azure
- Run security and quality checks
- Create container images and push them to container registries
- Ensure consistent and repeatable deployment processes

## Monitoring and Logging

### Azure Monitor
Azure Monitor is a comprehensive solution for collecting, analyzing, and acting on telemetry from cloud and on-premises environments. In this project, it provides:
- Centralized monitoring of all application components
- Infrastructure metrics collection
- Alert management
- Dashboard visualization

### Application Insights
Application Insights, a feature of Azure Monitor, is an application performance management (APM) service. In this project, it:
- Tracks live application performance
- Detects and diagnoses exceptions and performance issues
- Monitors user behavior and patterns
- Tracks distributed transactions across service boundaries
- Provides AI-powered analytics

### Log Analytics
Log Analytics is a tool in the Azure portal for editing and running log queries on data collected by Azure Monitor. In this project, it enables:
- Complex query capabilities across logs and metrics
- Custom reporting and visualization
- Troubleshooting application issues
- Performance analysis and optimization
- Correlation of events across different services

## Authentication and Security

### Azure Active Directory (Azure AD)
Azure Active Directory is Microsoft's cloud-based identity and access management service. In this project, it provides:
- User authentication for the frontend application
- Integration with Microsoft account logins
- Role-based access control
- Security token services
- Conditional access policies

### Microsoft Authentication Library (MSAL)
MSAL is a library that enables developers to acquire tokens from the Microsoft identity platform. In this project, it:
- Handles the authentication flow in the frontend application
- Manages token acquisition, caching, and renewal
- Implements OAuth 2.0 and OpenID Connect standards
- Provides secure access to protected backend APIs

## Storage

### Azure Blob Storage
Azure Blob Storage is Microsoft's object storage solution for the cloud. In this project, it's used to:
- Store uploaded documents like invoices
- Provide temporary storage for document processing
- Archive transaction records and receipts
- Store application assets and resources

## Development and Collaboration

### Visual Studio Code
Visual Studio Code is a lightweight but powerful source code editor. Recommended for this project because it:
- Provides excellent support for JavaScript, TypeScript, and Java
- Offers a rich extension ecosystem for development
- Includes integrated terminal and debugging capabilities
- Supports remote development and collaboration
- Integrates with Git for version control

### GitHub
GitHub is a web-based hosting service for version control using Git. In this project, it's used for:
- Source code management
- Collaborative development through pull requests and issues
- Integration with CI/CD workflows
- Documentation hosting
- Project management through issues and projects

## Frontend Tooling

### Vite
Vite is a modern frontend build tool that provides a faster and leaner development experience. In this project, it:
- Serves as the build system for the React application
- Provides hot module replacement for rapid development
- Optimizes assets for production
- Manages TypeScript compilation
- Handles environment variables and configuration

### Fluent UI
Fluent UI is Microsoft's design system for creating modern, intuitive user interfaces. In this project, it provides:
- Consistent design language across the application
- Accessible UI components
- Responsive design capabilities
- Theming and customization options
- Integration with React

## Miscellaneous

### NGINX
NGINX is a web server that can also be used as a reverse proxy, load balancer, and HTTP cache. In this project, it:
- Serves the frontend React application
- Handles request routing
- Manages HTTP headers and caching
- Provides TLS termination in container environments
- Optimizes static asset delivery

## Azure Developer CLI (azd)

Azure Developer CLI (azd) is a command-line tool that accelerates the time it takes to get started on Azure. In this project, it:
- Simplifies the end-to-end developer experience
- Provides templates for common application patterns
- Automates provisioning of Azure resources
- Streamlines deployment workflows
- Manages environment configuration
