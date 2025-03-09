# Multi Agents Sample Application with Java and Semantic Kernel

This application is designed to explore the capabilities of generative AI within the context of multi-agent architecture. By leveraging Java and Semantic Kernel, this project aim is to build a chat application that facilitates real-time communication among multiple agents.

## Description

### Application Overview

This application is a multi-agent banking assistant powered by Java and Semantic Kernel, demonstrating how generative AI can transform traditional banking interactions into natural language conversations. The system allows users to:

- Inquire about account balances and details
- Review transaction history and search for specific transactions
- Process payments and pay bills, including through invoice image uploads
- Verify payment methods and account funds before transactions

The application employs a vertical multi-agent architecture where specialized AI agents handle different domains of the banking experience:

1. **Router Agent** - The central coordinator that analyzes user intent from chat messages and routes conversations to the appropriate specialist agent
2. **Account Agent** - Provides information about bank accounts, balances, and payment methods
3. **Transaction History Agent** - Retrieves and presents transaction history with filtering capabilities
4. **Payment Agent** - Processes bill payments, including image-based invoice scanning using Azure Document Intelligence

Each agent is equipped with specific tools to interact with banking microservices through OpenAPI definitions, providing a seamless experience where users can accomplish banking tasks through natural conversation rather than navigating traditional web interfaces.

### Project Structure

The application follows a microservices architecture organized as follows:

```
app/
├── compose.yaml                # Docker Compose configuration for local deployment
├── start-compose.ps1           # PowerShell script to start services using Docker Compose
├── start-compose.sh            # Bash script to start services using Docker Compose
├── business-api/               # Backend business microservices
│   ├── account/                # Account management service
│   │   ├── Dockerfile          # Container definition for account service
│   │   ├── pom.xml             # Maven build configuration
│   │   └── src/                # Source code for account service
│   ├── payment/                # Payment processing service
│   │   ├── Dockerfile          # Container definition for payment service
│   │   ├── pom.xml             # Maven build configuration
│   │   └── src/                # Source code for payment service
│   └── transactions-history/   # Transaction history service
│       ├── Dockerfile          # Container definition for transaction history service
│       ├── pom.xml             # Maven build configuration
│       └── src/                # Source code for transaction history service
├── copilot/                    # Copilot service - AI orchestration layer
│   ├── Dockerfile              # Container definition for copilot service
│   ├── pom.xml                 # Maven parent build configuration
│   ├── copilot-backend/        # Main copilot service implementation
│   │   ├── pom.xml             # Maven build configuration
│   │   ├── manifests/          # Kubernetes manifests for deployment
│   │   └── src/                # Source code for copilot backend
│   └── semantickernel-openapi-plugin/ # Semantic Kernel OpenAPI plugin
│       ├── pom.xml             # Maven build configuration
│       └── src/                # Plugin source code
└── frontend/                   # User interface application
    ├── Dockerfile              # Container definition for production
    ├── Dockerfile-aks          # Container definition for AKS deployment
    ├── package.json            # NPM dependencies and scripts
    ├── tsconfig.json           # TypeScript configuration
    ├── vite.config.ts          # Vite build configuration
    ├── manifests/              # Kubernetes manifests for deployment
    ├── nginx/                  # NGINX configuration for serving frontend
    ├── public/                 # Static assets
    └── src/                    # React application source code
        ├── api/                # API client code
        ├── components/         # Reusable UI components
        ├── pages/              # Application pages
        └── assets/             # Frontend assets (images, styles)
```

The project consists of three main components:
1. **Business API Services** - A set of Java microservices that handle various business domains:
   - Account Service - Manages user account information
   - Payment Service - Processes payment transactions
   - Transaction History Service - Stores and retrieves transaction records

2. **Copilot Service** - The AI orchestration layer built with Java and Semantic Kernel:
   - Copilot Backend - Core backend service that integrates with Azure OpenAI
   - Semantic Kernel OpenAPI Plugin - Extends functionality through OpenAPI integration

3. **Frontend Application** - A React-based web interface built with:
   - React/TypeScript
   - Modern frontend tooling (Vite)
   - Containerized for deployment

### Architecture

```mermaid
flowchart TB
    User(User)--"Chat/Uploads"-->Frontend

    subgraph "Frontend Layer"
        Frontend[React Frontend Application]
    end

    Frontend--API Requests-->CopilotBackend

    subgraph "AI Orchestration Layer"
        CopilotBackend[Copilot Backend]

        subgraph "Multi-Agent System"
            RouterAgent[Router Agent\nAnalyzes Intent]
            PaymentAgent[Payment Agent]
            AccountAgent[Account Agent]
            TransactionAgent[Transaction History Agent]

            RouterAgent-->PaymentAgent
            RouterAgent-->AccountAgent
            RouterAgent-->TransactionAgent
        end

        CopilotBackend-->RouterAgent

        SemanticKernel[Semantic Kernel]
        OpenAPIPlugin[OpenAPI Plugin]

        PaymentAgent-->SemanticKernel
        AccountAgent-->SemanticKernel
        TransactionAgent-->SemanticKernel
        SemanticKernel-->OpenAPIPlugin
    end

    subgraph "Azure AI Services"
        AzureOpenAI[Azure OpenAI]
        AzureDocIntel[Azure Document Intelligence]
        AzureStorage[Azure Blob Storage]
    end

    subgraph "Business API Layer"
        AccountAPI[Account Service API]
        PaymentAPI[Payment Service API]
        TransactionAPI[Transaction History Service API]
    end

    OpenAPIPlugin-->AccountAPI
    OpenAPIPlugin-->PaymentAPI
    OpenAPIPlugin-->TransactionAPI

    CopilotBackend-->AzureOpenAI
    PaymentAgent-->AzureDocIntel
    AzureDocIntel-->AzureStorage

    style Frontend fill:#f9f9f9,stroke:#333,stroke-width:2px
    style CopilotBackend fill:#d1e7dd,stroke:#333,stroke-width:2px
    style RouterAgent fill:#d1e7dd,stroke:#333,stroke-width:2px
    style PaymentAgent fill:#d1e7dd,stroke:#333,stroke-width:2px
    style AccountAgent fill:#d1e7dd,stroke:#333,stroke-width:2px
    style TransactionAgent fill:#d1e7dd,stroke:#333,stroke-width:2px
    style AccountAPI fill:#dbeafe,stroke:#333,stroke-width:2px
    style PaymentAPI fill:#dbeafe,stroke:#333,stroke-width:2px
    style TransactionAPI fill:#dbeafe,stroke:#333,stroke-width:2px
    style AzureOpenAI fill:#fde68a,stroke:#333,stroke-width:2px
    style AzureDocIntel fill:#fde68a,stroke:#333,stroke-width:2px
    style AzureStorage fill:#fde68a,stroke:#333,stroke-width:2px
    style User fill:#fff,stroke:#333,stroke-width:2px
```

The architecture follows a vertical multi-agent design pattern where:

1. Users interact with the React frontend interface for natural language conversations and document uploads.
2. The Copilot Backend serves as the AI orchestration layer that hosts the multi-agent system.
3. A Router Agent analyzes user intent and delegates tasks to specialized domain agents:
   - Account Agent for handling account information requests
   - Transaction History Agent for retrieving transaction records
   - Payment Agent for processing payments and scanning invoices
4. Each agent uses Semantic Kernel to reason and execute operations via tools.
5. The OpenAPI Plugin maps natural language intents to structured API calls.
6. Business API services handle the actual banking operations.
7. Azure services provide the AI capabilities (Azure OpenAI) and document processing (Azure Document Intelligence).

This architecture enables a conversational interface to traditional banking services by leveraging AI to understand user intent and orchestrate appropriate actions across multiple specialized microservices.

## Demo

## Features

- feature:1
- feature:2

## Requirement

## Usage

## Installation

## References

- [Azure Samples - Agent OpenAI Java Banking Assistant](https://github.com/Azure-Samples/agent-openai-java-banking-assistant)

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/f3ac65a05ed8c8ea70b653875ccac0c6dbc10ba1/LICENSE)

## Author

- github: <https://github.com/shinyay>
- twitter: <https://twitter.com/yanashin18618>
- mastodon: <https://mastodon.social/@yanashin>
