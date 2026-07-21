# Software Engineering Handbook

This handbook outlines core software engineering principles, coding standards, and best practices for the GNUS.AI team. It is designed to be language-agnostic, applicable to technologies like TypeScript, Java, C++, Solidity, React, and others used in our blockchain and cryptography projects. These guidelines emphasize maintainable, readable code, adherence to SOLID principles, data-driven design, thorough unit testing, and responsible use of AI and code generation tools with human oversight. They align with expectations from engineer job descriptions (e.g., Senior Engineers mentoring on architecture, Junior Engineers building foundational habits) and project prompts emphasizing clear requirements, modularity, and iterative development.

### Preferred contributor guidelines

* Use the develop branch unless you are working on a major change that you think will be hard to fix breaking the develop branch, or is a major feature then use a feature branch and do a pull request to the develop branch.
* Use git rebase instead of merge [Here's Why](https://spin.atomicobject.com/2017/04/23/maintain-clean-git-history/)
* Pulls to master will be done on as-needed, since we operate on develop branches, this won't be very often.

### Git Rebase Workflows

Please read this blog about the appropriate way to use git rebase workflows.

[Git Rebase Workflow](https://nvie.com/posts/a-successful-git-branching-model/)

### Coding Standards

Follow these standards to ensure consistency, readability, and maintainability across all languages:

* **Naming Conventions**: Use descriptive, meaningful names. Prefer camelCase for variables/functions in TypeScript/Java; snake\_case for C++ where idiomatic. Constants should be UPPERCASE\_WITH\_UNDERSCORES.
* **Indentation and Formatting**: Use 4-space indentation (no tabs). Limit lines to 80-100 characters. Use tools like Prettier (TypeScript/JavaScript), clang-format (C++), or equivalent.
* **Comments and Documentation**: Write comments explaining "why," not "what." Use JSDoc (TypeScript), Javadoc (Java), or Doxygen (C++) for public APIs. Document Solidity contracts clearly.
* **Error Handling**: Handle errors explicitly with try-catch or equivalent. Avoid silent failures. In Solidity, use require/revert for preconditions.
* **Modularity**: Write small, reusable functions/modules (aim for <20-30 lines per function).
* **Performance**: Optimize only when profiling indicates need, especially in performance-critical C++ (e.g., cryptography). Prioritize security in blockchain code.
* **Version Control**: Commit frequently with descriptive messages. Use feature/bug branches, following Git Flow or similar.

These apply similarly to TypeScript, Java, C++, and other structured languages, adjusted for language idioms.

### SOLID Principles

Adhere to SOLID principles for flexible, maintainable object-oriented design:

* **Single Responsibility Principle (SRP)**: A class should have one reason to change. E.g., separate data access, business logic, and UI in React or Solidity contracts.
* **Open-Closed Principle (OCP)**: Classes should be open for extension, closed for modification. Use interfaces/abstract classes in Java/C++ or TypeScript types.
* **Liskov Substitution Principle (LSP)**: Subtypes must be substitutable for base types without breaking correctness. Ensure derived classes honor contracts.
* **Interface Segregation Principle (ISP)**: Prefer small, specific interfaces over large ones. In Solidity, design focused contract interfaces.
* **Dependency Inversion Principle (DIP)**: Depend on abstractions, not concretions. Program to interfaces, using design patterns or data-driven approaches (see below) to decouple dependencies.

Senior Engineers should mentor on SOLID in architectural decisions; Junior Engineers apply them daily.

### Data-Driven Design Principle

Prefer **data-driven design** over code-driven approaches to enhance flexibility and maintainability:

* **Programming to Interfaces**: Always code to interfaces or abstract types (e.g., `interface` in TypeScript/Java, pure virtual classes in C++). This supports loose coupling and aligns with DIP.
* **Loosely Coupled, Self-Contained Classes**: Design classes to minimize dependencies. Each class should manage its own data and behavior, interacting via well-defined interfaces.
* **Hierarchical Object Creation via Serialization**: Use data formats like XML or JSON to instantiate objects by ID or type, avoiding hardcoded type information. Classes should serialize/deserialize their own data, enabling child classes to do the same hierarchically.
  * **Example**: A C++ cryptography module could load a JSON config specifying an algorithm ID (e.g., AES), instantiate the corresponding class, and let it handle its own data serialization. In TypeScript/React, a component might load its state from JSON.
  * **Benefits**: Reduces tight coupling, supports dynamic object creation, and simplifies cross-language integration in blockchain systems.
* **Application**: Use this approach where possible, especially for systems requiring flexibility (e.g., plugin architectures, API-driven components).

### Design Pattern Standards

Design patterns from the Gang of Four (GoF) book complement SOLID principles, providing reusable solutions that promote loosely coupled, maintainable code. Use patterns judiciously to support project needs and SOLID goals:

* **Factory Method/Abstract Factory**: Supports OCP by enabling object creation without specifying concrete classes. Useful for creating families of related objects (e.g., cryptographic algorithms in C++).
* **Strategy**: Aligns with SRP and DIP by encapsulating interchangeable algorithms. E.g., switch between encryption strategies via an interface.
* **Observer**: Facilitates loose coupling for event-driven systems (e.g., React state updates, Solidity event listeners).
* **Adapter**: Bridges incompatible interfaces, supporting ISP and DIP (e.g., adapting legacy C++ code to a new TypeScript API).
* **Data-Driven Patterns**: Combine patterns like Factory with data-driven design. For example, use a Factory to instantiate objects from XML/JSON configs, ensuring classes are self-contained and serialize/deserialize their data.

Apply patterns that naturally fit the problem domain, prioritizing interface-driven, loosely coupled designs over rigid implementations.

### Code Generation Principle

Use **code generation tools** to accelerate development and ensure consistency across languages:

* **OpenAPI Specifications**: Define API schemas using OpenAPI (or similar) to generate client/server code for TypeScript, Java, C++, Solidity, etc. This ensures consistent interfaces and reduces manual coding errors.
  * **Example**: Generate TypeScript client code for a REST API or Solidity contract bindings from an OpenAPI spec, speeding up development significantly (up to 10x for cross-language projects).
* **Benefits**: Promotes standardization, reduces boilerplate, and supports rapid iteration in multi-language environments like blockchain systems.
* **Best Practices**: Write clear, comprehensive schemas. Validate generated code and customize as needed. Integrate with CI/CD for automation.

### Unit Testing

Unit tests ensure code reliability and prevent regressions:

* **Coverage**: Target 80%+ coverage for critical paths, including edge cases, happy paths, and failures.
* **Frameworks**: Use Jest (TypeScript/React), JUnit (Java), Google Test (C++), Hardhat/Truffle (Solidity).
* **Best Practices**: Prefer Test-Driven Development (TDD) where feasible. Keep tests isolated, fast, deterministic. Mock dependencies.
* **AI Tools**: Use Grok, Claude.ai, or ChatGPT to generate test skeletons or ideas, but always review manually—AI can miss edge cases or context. Human intervention is critical.
* **Integration**: Run tests in CI/CD pipelines. Fail builds on test failures.

### Leveraging AI Tools

AI accelerates development but requires responsibility:

* **Usage**: Use AI for code generation, debugging suggestions, or crafting project prompts. Follow our prompt engineering guidelines: specify requirements, constraints, and expected outputs clearly.
* **Human Oversight**: Always verify AI outputs, especially for unit tests, cryptography, or complex logic, as AI may produce errors or hallucinations.
* **Prompt Engineering**: Write detailed prompts (as per past project examples) to ensure accurate outputs.

### General Software Development Principles

From engineer job descriptions and project expectations:

* **Proactive Problem-Solving**: Anticipate issues and propose solutions independently.
* **Collaboration**: Engage in code reviews, providing constructive feedback.
* **Continuous Learning**: Stay current with technologies (React, Solidity, C++ cryptography).
* **Maintainability**: Prioritize clean, modular code over quick fixes.

### Language-Specific Standards

#### C++ Coding Standards

{% content-ref url="c++-coding-standards.md" %}
[c++-coding-standards.md](c++-coding-standards.md)
{% endcontent-ref %}

### Python Coding Standards

{% content-ref url="c++-coding-standards.md" %}
[python-coding-standards.md](python-coding-standards.md)
{% endcontent-ref %}

### Typescript Coding Standards

{% content-ref url="typescript-coding-standards.md" %}
[typescript-coding-standards.md](typescript-coding-standards.md)
{% endcontent-ref %}

#### Smart Contract Projects

{% content-ref url="smart-contract-projects.md" %}
[smart-contract-projects.md](smart-contract-projects.md)
{% endcontent-ref %}