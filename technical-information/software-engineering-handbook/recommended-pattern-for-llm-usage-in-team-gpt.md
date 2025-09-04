---
description: >-
  This page outlines best practices for leveraging Large Language Models (LLMs)
  within Team-GPT to optimize software engineering workflows, particularly for
  architecture design, code generation, and pro
---

# Recommended Pattern for LLM Usage in Team-GPT

### Architecture Planning

When planning the high-level architecture or summary design of a project:

* Use the following LLMs in this preferred order for generating architectural summaries:
  1. **gpt-oss-20b** (primary choice for open-source efficiency).
  2. **Grok 4** (reliable and versatile).
  3. **Claude Opus 4.1** (strong for complex reasoning).
  4. **ChatGPT 5** (as a fallback for advanced capabilities).
* Instruct these LLMs explicitly **not to generate code**. Their role is limited to providing architectural overviews, diagrams, or high-level designs without delving into implementation details.
* If the initial architecture needs refinement or you encounter limitations, switch to **Grok Code Fast** for quick iterations. This model is extremely cost-effective but may be less accurate, so validate outputs carefully.
* For troubleshooting or alternative perspectives, cycle through these models:
  * **Qwen Code 3** (free, but slower with a good parameter size for detailed reasoning).
  * **Grok Code Fast** (fast and inexpensive, though prone to occasional errors).
  * **Claude Sonnet 4** (moderately priced and reliable for balanced performance).

Avoid using **Claude Opus**, **GROK 4**, or **ChatGPT 5** for any code-related tasks, as they are not optimized for code generation and incur higher costs.

### Code Generation

Once the architecture is outlined:

* Switch to specialized code generation LLMs, such as **Grok Code Fast** or **Qwen Code 3**, for producing actual code.
* Instruct these LLMs to **generate code without placeholders**. This ensures complete, ready-to-use code rather than partial or templated outputs.
* Do not use architecture-focused models (e.g., Claude Opus, GROK 4, or ChatGPT 5) for this step, as they are inefficient and expensive for code tasks.

#### Integration with Project Knowledge

* When creating a new chat for code generation, ensure it includes **project instructions**. Copy these from existing practices for a C++ senior software engineer (e.g., coding standards, best practices, and guidelines) and add them to the project's knowledge base.
* Reference the **ThirdParty\_Libraries\_Integration.md** file to inform the LLM about approved C++ libraries and integration patterns. Include this file in the project knowledge for any new projects to maintain consistency.

### Testing and Validation

* After code generation, use the coding LLM (e.g., Grok Code Fast or Qwen Code 3) to **write GTests** (Google Test framework tests) for the generated code.
* Ensure tests are comprehensive, drawing from the project's knowledge base, including architecture summaries and library integrations.

### Project and Chat Setup

* **New Projects**: When starting a new project, populate the project knowledge with:
  * A description of the project.
  * Copied instructions from established C++ senior software engineer practices.
  * The **ThirdParty\_Libraries\_Integration.md** file for library details.
  * Any relevant files or linked chats.
* **Chats Under Projects**: If creating sub-chats within an existing project, they will automatically source context from:
  * The project's knowledge description.
  * Attached files (e.g., architecture docs, library integrations).
  * Linked chats for continuity and shared context.

This pattern promotes a structured workflow: start with high-level architecture using cost-effective reasoning models, transition to efficient code generators, and ensure testing and project consistency through integrated knowledge. Always monitor for accuracy and switch models as needed to balance speed, cost, and quality.
