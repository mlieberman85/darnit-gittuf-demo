# Architecture

## Overview

This document describes the architecture and design of darnit-gittuf-demo, including its major components, the actors that interact with it, and how data flows through the system.

## Components

| Component | Path |
|-----------|------|
| internal | `internal/` |
| &nbsp;&nbsp;attestations | `internal/attestations/` |
| &nbsp;&nbsp;cache | `internal/cache/` |
| &nbsp;&nbsp;cmd | `internal/cmd/` |
| &nbsp;&nbsp;common | `internal/common/` |
| &nbsp;&nbsp;dev | `internal/dev/` |
| &nbsp;&nbsp;display | `internal/display/` |
| &nbsp;&nbsp;git-remote-gittuf | `internal/git-remote-gittuf/` |
| &nbsp;&nbsp;luasandbox | `internal/luasandbox/` |
| &nbsp;&nbsp;policy | `internal/policy/` |
| &nbsp;&nbsp;rsl | `internal/rsl/` |
| &nbsp;&nbsp;signerverifier | `internal/signerverifier/` |
| &nbsp;&nbsp;testartifacts | `internal/testartifacts/` |
| &nbsp;&nbsp;third_party | `internal/third_party/` |
| &nbsp;&nbsp;tuf | `internal/tuf/` |
| &nbsp;&nbsp;version | `internal/version/` |
| pkg | `pkg/` |
| &nbsp;&nbsp;gitinterface | `pkg/gitinterface/` |

> Update this table to reflect the actual responsibilities of each component.

## Actors

| Actor | Description | Interactions |
|-------|-------------|-------------|
| End User | Primary user of the software | Sends requests via CLI/API, receives results |
| Administrator | Manages configuration and deployment | Configures system, manages access |
| CI/CD System | Automated build and deployment pipeline | Triggers builds, runs tests, deploys |
| External Services | Third-party APIs or dependencies | Provides data or services consumed by the system |

## Data Flow

```
End User → API Layer → Core Engine → Storage
                ↓
         Configuration
                ↓
         External Services
```

1. **Input**: User submits a request through the API layer (CLI, HTTP, or library call)
2. **Validation**: The API layer validates input parameters and authentication
3. **Processing**: The core engine processes the request using configured rules
4. **Storage**: Results are persisted to the storage layer
5. **Response**: Processed results are returned to the user

## Security Boundaries

- **External boundary**: All user input is validated at the API layer
- **Internal boundary**: Storage access is mediated through the core engine
- **Trust boundary**: External service calls use authenticated connections