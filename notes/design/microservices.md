# Microservices
- architectural style that structures an application using **loosely coupled services**
- independently deployable modules
- opposite of _monolithic_ architecture
- split by
    - domain (business logic)
    - technical reasons (need for independent scaling, different technologies, ...)
- greenfield vs. splitting the monolith

## Sources
- [Domain-Driven Design Distilled](https://www.amazon.com/dp/B01JJSGE5S) (168 pages)
- [What are microservices?](https://www.educative.io/edpresso/what-are-microservices) (Educative edpresso)
- [Microservices architecture tutorial: All you need to get started](https://www.educative.io/blog/microservices-architecture-tutorial-all-you-need-to-get-started) (Educative blog)

## Tradeoffs

### Pros
- scalability of individual services (CPU, memory)
- scalability of development process - teams own individual services
    - smaller codebase - less spaghetti code due to strong isolation (decoupling), faster builds
    - independent release/lifecycle (easier changes to the system)
        - facilitates continuous delivery
    - teams can use different stacks
- resilience - service outage shouldn't bring the whole system down

### Cons
- lots of complexity in testing, deploying and running the microservices (operations)
    - **prerequisites**
        - automation (tests, deployment, scaling, ...)
        - central logging
        - monitoring
            - distributed tracing
        - independent testing and deployment (backward compatible APIs)
- achieving strong consistency is not easy
- changes to multiple microservices might require coordination
- increased latency
- communication between microservices is unreliable - effort to make it resilient

## Micro and Macro architecture
- **micro architecture** - on individual service level
- **macro architecture** - overall all services together (cross-service)
    - flexibility to **change one module without influencing the other**
        - no shared code
        - no shared database

### Domain-driven design
- collection of patterns for the domain model of a system
- **premise**: microservices (modules) require different **domain models**
    - customer could be required for many microservices, but perhaps with different attributes
- **bounded context** - each domain model is valid only in a bounded context
    - implement as a microservice or just a module
    - eshop example: search, catalog, order, payment, ...
- **domain event** - communication between bounded contexts

#### Patterns
- customer-supplier - strong dependency, better to avoid if possible
- conformist - uses domain model from a different bounded context but has no authority to change it
    - for example statistics
- separate ways - no communication on technical level
- open host - publishes API for many services

## Architecture decisions
- don't enforce many rules on macro level, give teams independence
- document reasons for each rule

### Micro or macro (tradeoffs)
- programming language and framework
- database - always isolate at least on the schema level
    - single database with different schemas
    - multiple instances of the same database
    - different databases
- UI
- documentation
- delivery pipeline (CI&CD)

### Macro
- communication protocol
- authentication
- integration tests
- operations
    - configuration and secrets
    - monitoring, alerting
    - logging, tracing

### Micro
- authorization
- module tests
- operations
    - metrics definition
    - more freedom if teams own the service end-to-end

## Independent Systems Architecture (ISA) principles
- The system must be divided into modules that offer interfaces.
- The system must have two clearly separated levels of architectural decisions: macro and micro.
- Modules must be separate processes, containers, or virtual machines to maximize independence.
- The choice of integration and communication options must be limited and standardized for the system.
- Metadata, for example, for _authentication_, must be standardized.
- Each module must have its own independent continuous delivery pipeline.
- Operations **should** be standardized.
- Standards for operations, integration, or communication should be enforced on the **interface level**.
- Modules have to be resilient.

## Observability
- must have not just for microservices
- ability to measure the internal state of a system by examining its outputs
- topics
    - **logs** (centralized)
    - **metrics**
    - **distributed tracing**
        - open standard OpenTracing (nowadays replaced with **OpenTelemetry**)
            - implemented by NewRelic, AppDynamics, ..
        - trace is a span that represents an execution of code (spanning multiple services)
- preferably all covered by a single tool (Splunk, NewRelic, AppDynamics)

## Service discovery
- helps us know where each instance is located
- acts as a **registry** in which the addresses of all instances are tracked
    - **client-side**
        - consumer queries the registry and handles load-balancing, there is no extra hop (no load balancer)
        - need to implement for all languages
    - **server-side**
        - an intermediary that acts as a load balancer
        - the logic is in one place, but there is an extra hop