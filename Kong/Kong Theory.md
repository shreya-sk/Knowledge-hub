> Resources
 [ ] https://github.com/grongierisc/kong-ee-training?tab=readme-ov-file#1-intersystems-api-manager-training
> - 
# Kong Gateway

Kong Gateway is an API Gateway solution built as a Lua application. It operates within nginx, utilizing workers to provide its feature set. The architecture flows as:

Sonic Commercial API → Kong → Kubernetes Servers
## Core Components

### Kong Control Plane (Infrastructure)

- Houses the Kong Manager UI
- Manages configuration and administrative functions
- Data planes uses the config defined in control plane to redirect to the 

### Kong Data Plane (Application)

- Handles the actual API traffic
- Executes policies and routes requests

## Administrative Interfaces

### Kong Admin API

- RESTful interface for administration
- Used for CI/CD automation
- Enables programmatic control of Kong configurations

### Kong Manager

- Graphical user interface for gateway management
- Provides visualization and control of routes and services

### decK

- Configuration management tool for Kong Gateway
- Helps manage Kong's gateway services
- Enables version control of configurations

## Key Concepts

### Services

- Entities representing external upstream APIs or microservices
- The actual destination where Kong forwards requests
- Think of a Service as the address of a restaurant you want to visit

### Routes

- Define how requests are sent to Services
- Determined by paths, hosts, headers, and other conditions
- Routes are associated with specific Services
- Support advanced pattern matching using regex
- Can be versioned (e.g., /v1/users, /v2/users)
- Multiple Routes can point to the same Service

- **Routes** are like the sorting rules that determine which packages (requests) go where
- Each package has an address label (URL path, HTTP method, headers)
- The sorting clerk (Kong) reads these labels and directs the package to the right delivery truck
- **Services** are like the final destinations (the actual API endpoints)
- Different packages might take different routes but end up at the same destination

### Consumers

- Represent users of your API
- Can be associated with credentials for authentication
- Enable personalized rate limiting and access controls

**Think of Consumers as members of a private club:**

- Each member has their own membership card (API key or credentials)
- The doorman (Kong) checks these cards before allowing entry
- Different members have different privileges (rate limits, accessible areas)
- The club keeps track of how often each member visits (analytics)
-