# Fixers - A Comprehensive Kotlin Framework Suite

Fixers is a collection of modular frameworks and tools designed to simplify and accelerate the development of robust, scalable applications using Kotlin and related technologies. Each module in the Fixers ecosystem addresses specific aspects of modern application development, from backend services to frontend UI components, documentation, and build automation.

## Project Modules

### [fixers-gradle](https://github.com/komune-io/fixers-gradle)
A toolkit designed to make setting up and managing Kotlin projects easier through:
- Gradle plugins for common configurations
- Static code analysis and quality checks
- Artifact publishing system
- Make-driven reusable workflows
- GitHub composite actions
- Automated versioning system
- Documentation and Storybook workflow

### [fixers-f2](https://github.com/komune-io/fixers-f2)
A **Kotlin-based framework** for building event-driven applications using a functional programming style, particularly suited for the CQRS (Command Query Responsibility Segregation) pattern. Features include:
- Functional primitives (F2Supplier, F2Function, F2Consumer)
- Spring Cloud Function integration
- Protocol adapters for HTTP and RSocket
- Standardized message wrappers
- Client abstractions
- Comprehensive error handling

### [fixers-c2](https://github.com/komune-io/fixers-c2)
A framework for implementing **Signing State Machines (SSMs)** - digital workflows where multiple parties can securely and verifiably change shared data according to predefined rules. Built on Hyperledger Fabric blockchain, it provides:
- Secure digital signature workflows
- REST API Gateway for external applications
- SDKs for integration
- CouchDB integration for rich queries

### [fixers-s2](https://github.com/komune-io/fixers-s2)
A Kotlin framework for modeling state changes over time using Finite State Machines (FSMs). It offers:
- State machine definition and execution
- Commands and Events as interaction primitives
- Guards for transition pre-conditions
- Persistence layer
- Support for Event Sourcing and State Storing patterns
- Spring integration adapters

### [fixers-d2](https://github.com/komune-io/fixers-d2)
A tool that automatically generates **interactive documentation** for Kotlin projects, specifically formatted for Storybook. It extends Dokka (Kotlin's documentation engine) with:
- Custom KDoc tags for documentation structure
- Specialized D2StorybookPlugin
- MDX file generation for Storybook display
- Gradle plugin for easy integration

### [fixers-g2](https://github.com/komune-io/fixers-g2)
A **library of reusable UI components** and related systems for building web application frontends. Components include:
- UI component system
- Theming system
- Layout system
- Form abstractions
- Table system
- Identity management abstractions
- Storybook configuration
- Build automation

## How the Modules Relate

The Fixers ecosystem is designed to be modular yet integrated:

- **fixers-gradle** provides the foundation for building, testing, and deploying all other modules
- **fixers-f2** offers functional programming primitives that can be used by other modules
- **fixers-c2** implements blockchain-based workflows that can utilize the state machine concepts from fixers-s2
- **fixers-s2** provides state machine abstractions that can be leveraged by business logic in applications
- **fixers-d2** generates documentation for all modules, creating a consistent documentation experience
- **fixers-g2** offers UI components that can be used to build frontends for applications using the other modules

## Getting Started

To use any of the Fixers modules, visit the respective GitHub repository for detailed installation and usage instructions:

- [fixers-gradle](https://github.com/komune-io/fixers-gradle)
- [fixers-f2](https://github.com/komune-io/fixers-f2)
- [fixers-c2](https://github.com/komune-io/fixers-c2)
- [fixers-s2](https://github.com/komune-io/fixers-s2)
- [fixers-d2](https://github.com/komune-io/fixers-d2)
- [fixers-g2](https://github.com/komune-io/fixers-g2)

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

Individual modules may have their own specific licensing information. Please refer to each module's repository for details.

## Contributing

Contributions to any of the Fixers modules are welcome. Please refer to the contributing guidelines in each repository for more information.
