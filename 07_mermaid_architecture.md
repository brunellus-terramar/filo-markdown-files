# Software Architecture: E-Commerce Platform

This document demonstrates Mermaid diagrams for visualizing software architecture.

## System Overview

```mermaid
graph TB
    subgraph "Client Layer"
        WEB[Web App]
        MOBILE[Mobile App]
        ADMIN[Admin Dashboard]
    end
    
    subgraph "API Gateway"
        GW[Kong Gateway]
        AUTH[Auth Service]
    end
    
    subgraph "Microservices"
        USER[User Service]
        PRODUCT[Product Service]
        ORDER[Order Service]
        PAYMENT[Payment Service]
        INVENTORY[Inventory Service]
        NOTIFY[Notification Service]
    end
    
    subgraph "Data Layer"
        POSTGRES[(PostgreSQL)]
        REDIS[(Redis Cache)]
        ELASTIC[(Elasticsearch)]
        S3[(S3 Storage)]
    end
    
    subgraph "Message Queue"
        KAFKA[Apache Kafka]
    end
    
    WEB --> GW
    MOBILE --> GW
    ADMIN --> GW
    GW --> AUTH
    GW --> USER
    GW --> PRODUCT
    GW --> ORDER
    GW --> PAYMENT
    GW --> INVENTORY
    
    USER --> POSTGRES
    PRODUCT --> POSTGRES
    ORDER --> POSTGRES
    PAYMENT --> POSTGRES
    INVENTORY --> POSTGRES
    
    PRODUCT --> ELASTIC
    USER --> REDIS
    PRODUCT --> REDIS
    PRODUCT --> S3
    
    ORDER --> KAFKA
    PAYMENT --> KAFKA
    KAFKA --> NOTIFY
    KAFKA --> INVENTORY
```

## Class Diagram: Order Domain

```mermaid
classDiagram
    class Order {
        +String orderId
        +Date createdAt
        +OrderStatus status
        +Customer customer
        +List~OrderItem~ items
        +calculateTotal() Decimal
        +addItem(item: OrderItem)
        +removeItem(itemId: String)
        +updateStatus(status: OrderStatus)
    }
    
    class OrderItem {
        +String itemId
        +Product product
        +int quantity
        +Decimal unitPrice
        +getSubtotal() Decimal
    }
    
    class Product {
        +String productId
        +String name
        +String description
        +Decimal price
        +int stockQuantity
    }
    
    class Customer {
        +String customerId
        +String email
        +String name
        +Address shippingAddress
        +Address billingAddress
    }
    
    class Address {
        +String street
        +String city
        +String state
        +String postalCode
        +String country
    }
    
    class OrderStatus {
        <<enumeration>>
        PENDING
        CONFIRMED
        PROCESSING
        SHIPPED
        DELIVERED
        CANCELLED
    }
    
    Order "1" --> "1" Customer
    Order "1" --> "*" OrderItem
    OrderItem "1" --> "1" Product
    Customer "1" --> "1" Address : shipping
    Customer "1" --> "1" Address : billing
    Order --> OrderStatus
```

## Sequence Diagram: Checkout Flow

```mermaid
sequenceDiagram
    participant C as Customer
    participant W as Web App
    participant G as API Gateway
    participant O as Order Service
    participant P as Payment Service
    participant I as Inventory Service
    participant N as Notification Service
    
    C->>W: Click Checkout
    W->>G: POST /orders
    G->>O: Create Order
    O->>I: Check Inventory
    I-->>O: Items Available
    O->>P: Process Payment
    P-->>O: Payment Confirmed
    O->>I: Reserve Items
    I-->>O: Items Reserved
    O-->>G: Order Created
    G-->>W: Order Confirmation
    W-->>C: Display Confirmation
    
    Note over O,N: Async via Kafka
    O-)N: Order Event
    N-)C: Email Confirmation
```

## Entity Relationship Diagram

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    CUSTOMER {
        uuid id PK
        string email UK
        string name
        timestamp created_at
    }
    
    ORDER ||--|{ ORDER_ITEM : contains
    ORDER {
        uuid id PK
        uuid customer_id FK
        string status
        decimal total
        timestamp created_at
    }
    
    ORDER_ITEM }|--|| PRODUCT : references
    ORDER_ITEM {
        uuid id PK
        uuid order_id FK
        uuid product_id FK
        int quantity
        decimal unit_price
    }
    
    PRODUCT ||--o{ PRODUCT_CATEGORY : "belongs to"
    PRODUCT {
        uuid id PK
        string name
        text description
        decimal price
        int stock_quantity
    }
    
    CATEGORY ||--o{ PRODUCT_CATEGORY : contains
    CATEGORY {
        uuid id PK
        string name
        uuid parent_id FK
    }
    
    PRODUCT_CATEGORY {
        uuid product_id FK
        uuid category_id FK
    }
```

## Deployment Architecture

```mermaid
graph TB
    subgraph "AWS Cloud"
        subgraph "VPC"
            subgraph "Public Subnet"
                ALB[Application Load Balancer]
                NAT[NAT Gateway]
            end
            
            subgraph "Private Subnet - App"
                EKS[EKS Cluster]
                subgraph "Pods"
                    P1[User Service]
                    P2[Product Service]
                    P3[Order Service]
                    P4[Payment Service]
                end
            end
            
            subgraph "Private Subnet - Data"
                RDS[(RDS PostgreSQL)]
                ELASTICACHE[(ElastiCache Redis)]
                MSK[MSK Kafka]
            end
        end
        
        S3_BUCKET[S3 Bucket]
        CLOUDFRONT[CloudFront CDN]
        ROUTE53[Route 53]
    end
    
    INTERNET((Internet)) --> ROUTE53
    ROUTE53 --> CLOUDFRONT
    CLOUDFRONT --> ALB
    ALB --> EKS
    EKS --> RDS
    EKS --> ELASTICACHE
    EKS --> MSK
    EKS --> S3_BUCKET
```

## Summary

This architecture demonstrates:
- **Microservices**: Loosely coupled services with single responsibilities
- **Event-driven**: Kafka for async communication between services
- **Caching**: Redis for performance optimization
- **Search**: Elasticsearch for product search
- **Cloud-native**: Containerized deployment on Kubernetes
