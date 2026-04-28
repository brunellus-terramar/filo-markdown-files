# Process Flowcharts and State Diagrams

This document demonstrates various Mermaid diagram types for process visualization.

## User Registration Flowchart

```mermaid
flowchart TD
    START([Start]) --> INPUT[User enters email]
    INPUT --> VALIDATE{Valid email format?}
    VALIDATE -->|No| ERROR1[Show format error]
    ERROR1 --> INPUT
    VALIDATE -->|Yes| CHECK{Email exists?}
    CHECK -->|Yes| ERROR2[Email already registered]
    ERROR2 --> LOGIN[Redirect to login]
    CHECK -->|No| PASSWORD[Enter password]
    PASSWORD --> STRENGTH{Password strong?}
    STRENGTH -->|No| ERROR3[Show requirements]
    ERROR3 --> PASSWORD
    STRENGTH -->|Yes| VERIFY[Send verification email]
    VERIFY --> WAIT{User clicks link?}
    WAIT -->|Timeout| RESEND[Resend option]
    RESEND --> VERIFY
    WAIT -->|Yes| ACTIVATE[Activate account]
    ACTIVATE --> WELCOME[Show welcome page]
    WELCOME --> FINISH([End])
```

## Order State Machine

```mermaid
stateDiagram-v2
    [*] --> Draft: Create order
    
    Draft --> Submitted: Submit order
    Draft --> Cancelled: Cancel
    
    Submitted --> PaymentPending: Process payment
    Submitted --> Cancelled: Cancel
    
    PaymentPending --> PaymentFailed: Payment declined
    PaymentPending --> Confirmed: Payment success
    
    PaymentFailed --> PaymentPending: Retry payment
    PaymentFailed --> Cancelled: Cancel
    
    Confirmed --> Processing: Begin fulfillment
    Confirmed --> Refunded: Full refund
    
    Processing --> Shipped: Ship order
    Processing --> Refunded: Cancel & refund
    
    Shipped --> Delivered: Confirm delivery
    Shipped --> Returned: Return initiated
    
    Delivered --> Returned: Return request
    Delivered --> Completed: After return period
    
    Returned --> Refunded: Process refund
    
    Refunded --> [*]
    Cancelled --> [*]
    Completed --> [*]
```

## CI/CD Pipeline

```mermaid
flowchart LR
    subgraph "Development"
        COMMIT[Git Commit] --> PR[Pull Request]
    end
    
    subgraph "CI Pipeline"
        PR --> LINT[Lint Check]
        LINT --> TEST[Unit Tests]
        TEST --> BUILD[Build]
        BUILD --> SCAN[Security Scan]
    end
    
    subgraph "CD Pipeline"
        SCAN --> DEV[Deploy to Dev]
        DEV --> INT_TEST[Integration Tests]
        INT_TEST --> STAGING[Deploy to Staging]
        STAGING --> E2E[E2E Tests]
        E2E --> APPROVE{Manual Approval}
        APPROVE -->|Approved| PROD[Deploy to Production]
        APPROVE -->|Rejected| ROLLBACK[Rollback]
    end
    
    PROD --> MONITOR[Monitor & Alert]
```

## Decision Tree: Support Ticket Routing

```mermaid
flowchart TD
    TICKET[New Support Ticket] --> CAT{Category?}
    
    CAT -->|Billing| BILLING_CHECK{Amount disputed?}
    BILLING_CHECK -->|> $1000| SENIOR_BILLING[Senior Billing Agent]
    BILLING_CHECK -->|<= $1000| BILLING_AGENT[Billing Agent]
    
    CAT -->|Technical| TECH_CHECK{Product type?}
    TECH_CHECK -->|Enterprise| ENTERPRISE_SUPPORT[Enterprise Support Team]
    TECH_CHECK -->|Standard| PRIORITY{Priority?}
    PRIORITY -->|Critical| L2_SUPPORT[L2 Support]
    PRIORITY -->|Normal| L1_SUPPORT[L1 Support]
    
    CAT -->|Sales| SALES_CHECK{Existing customer?}
    SALES_CHECK -->|Yes| ACCOUNT_MANAGER[Account Manager]
    SALES_CHECK -->|No| SALES_REP[Sales Representative]
    
    CAT -->|General| BOT[Chatbot Response]
    BOT --> RESOLVED{Resolved?}
    RESOLVED -->|Yes| CLOSE[Close Ticket]
    RESOLVED -->|No| L1_SUPPORT
```

## Gantt Chart: Project Timeline

```mermaid
gantt
    title Product Launch Timeline
    dateFormat  YYYY-MM-DD
    
    section Planning
    Requirements gathering     :done,    req, 2024-01-01, 2024-01-14
    Technical design          :done,    design, 2024-01-15, 2024-01-28
    Resource allocation       :done,    resource, 2024-01-22, 2024-01-28
    
    section Development
    Backend API development   :active,  api, 2024-02-01, 2024-03-15
    Frontend development      :active,  frontend, 2024-02-15, 2024-03-31
    Database setup            :done,    db, 2024-02-01, 2024-02-14
    Third-party integrations  :         integrate, 2024-03-01, 2024-03-21
    
    section Testing
    Unit testing              :         unit, 2024-03-15, 2024-03-28
    Integration testing       :         int_test, 2024-03-25, 2024-04-07
    UAT                       :         uat, 2024-04-01, 2024-04-14
    Performance testing       :         perf, 2024-04-08, 2024-04-14
    
    section Launch
    Beta release              :milestone, beta, 2024-04-15, 1d
    Bug fixes                 :         fixes, 2024-04-15, 2024-04-28
    Production deployment     :milestone, prod, 2024-05-01, 1d
    Post-launch monitoring    :         monitor, 2024-05-01, 2024-05-14
```

## Pie Chart: Bug Distribution

```mermaid
pie showData
    title Bug Distribution by Severity
    "Critical" : 5
    "High" : 15
    "Medium" : 35
    "Low" : 45
```

## Git Workflow

```mermaid
gitGraph
    commit id: "Initial commit"
    branch develop
    checkout develop
    commit id: "Setup project"
    branch feature/auth
    checkout feature/auth
    commit id: "Add login"
    commit id: "Add registration"
    checkout develop
    merge feature/auth id: "Merge auth"
    branch feature/dashboard
    checkout feature/dashboard
    commit id: "Add dashboard UI"
    commit id: "Add charts"
    checkout develop
    merge feature/dashboard id: "Merge dashboard"
    checkout main
    merge develop id: "Release v1.0" tag: "v1.0.0"
    checkout develop
    branch hotfix/security
    checkout hotfix/security
    commit id: "Fix XSS vulnerability"
    checkout main
    merge hotfix/security id: "Hotfix" tag: "v1.0.1"
    checkout develop
    merge hotfix/security
```

## User Journey Map

```mermaid
journey
    title Customer Purchase Journey
    section Discovery
      Search for product: 5: Customer
      Browse categories: 3: Customer
      Read reviews: 4: Customer
    section Evaluation
      Compare prices: 4: Customer
      Check specifications: 3: Customer
      Add to wishlist: 4: Customer
    section Purchase
      Add to cart: 5: Customer
      Enter shipping info: 2: Customer
      Complete payment: 3: Customer
    section Post-Purchase
      Receive confirmation: 5: Customer, System
      Track shipment: 4: Customer
      Receive delivery: 5: Customer
      Leave review: 3: Customer
```

## Summary

This document showcases Mermaid's versatility:
- **Flowcharts**: Process flows and decision trees
- **State diagrams**: State machines and transitions
- **Gantt charts**: Project timelines
- **Pie charts**: Data distribution
- **Git graphs**: Version control visualization
- **Journey maps**: User experience flows

Mermaid enables teams to create maintainable diagrams as code, keeping documentation in sync with development.
