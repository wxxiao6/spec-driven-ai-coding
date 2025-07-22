

# **Deconstructing Kiro: A Blueprint for Architecting Spec-Driven Agentic Workflows in Custom IDEs**

## **Introduction: The Kiro Paradigm – From AI Assistant to AI Architect**

The landscape of software development is undergoing a profound transformation, driven by the integration of artificial intelligence into the core developer workflow. This evolution has progressed from simple code completion to sophisticated, conversational AI partners. However, the introduction of Amazon Web Services' (AWS) Kiro represents not an incremental improvement upon existing tools, but a fundamental paradigm shift. Kiro redefines the relationship between the developer and the AI, moving beyond the reactive, prompt-response cycle of what has been termed "vibe coding" to a proactive, structured, and collaborative process of software architecture.1 This approach aims to produce "viable code"—software that is not only functional but also documented, maintainable, and production-ready from its inception.3

The mission underpinning Kiro is to address a critical vulnerability in the burgeoning field of AI-assisted development: the proliferation of undocumented, difficult-to-maintain, and often misaligned AI-generated code.3 To combat this, Kiro integrates the rigor of enterprise-grade software development lifecycle (SDLC) methodologies directly into its agentic workflow. This system is explicitly modeled on the internal processes employed by software development teams at Amazon for managing large, complex technical projects, emphasizing planning, documentation, and architectural clarity as prerequisites to implementation.4

Where many AI tools act as a pair programmer, Kiro assumes the role of a junior architect or a small development team. It requires explicit, structured direction and, in return, delivers a comprehensive set of artifacts that document its understanding, its plan, and its execution. This philosophy creates a clear distinction between Kiro and other prominent AI development tools.

* **GitHub Copilot** operates primarily as a powerful, token-level autocomplete engine. Its strength lies in predicting the next line or block of code based on the immediate context of a single file, significantly boosting developer productivity but remaining limited in its scope and strategic capability.6  
* **Cursor**, an AI-native IDE, elevates this interaction. It excels at multi-file refactoring, codebase-aware chat, and executing complex, user-directed commands across a project.8 However, its workflow remains fundamentally reactive, responding to explicit prompts and instructions from the developer rather than formulating its own comprehensive plans.  
* **Kiro**, in contrast, is an "agentic IDE" that imposes a structured, goal-oriented workflow.6 It is designed to take a high-level, natural language description of a feature—such as "add user authentication"—and autonomously investigate the codebase, formulate a detailed plan, and then execute that plan across multiple files.6 It functions as a "structure enforcer," prioritizing planning, design, and quality assurance in a unified, AI-supported loop.7

This distinction in philosophy and operation is critical for understanding Kiro's unique value proposition. The following table provides a comparative analysis of these development paradigms, establishing a baseline for the detailed deconstruction that follows.

**Table 1: Comparative Analysis of AI Development Paradigms**

| Feature/Philosophy | GitHub Copilot | Cursor | Kiro (AWS) |
| :---- | :---- | :---- | :---- |
| **Core Paradigm** | Autocomplete | Chat-driven Refactoring | Spec-Driven Agentic Development |
| **Primary Interaction Model** | In-line suggestions | Chat prompts & commands | Goal descriptions & Spec approval |
| **Context Scope** | Single file, immediate context | Multi-file, user-provided context | Whole-project, persistent context (Specs \+ Steering) |
| **Workflow** | Reactive | Reactive/Interactive | Proactive & Structured (Plan \-\> Execute) |
| **Key Artifacts** | Generated code | Chat history & diffs | requirements.md, design.md, tasks.md, Steering files |
| **Developer Role** | Coder with assistant | Coder with conversational partner | Architect/PM reviewing agent's work |

## **Section 1: The Engine of Structure: Spec-Driven Development**

At the heart of Kiro's methodology is a systematic, agentic reasoning loop that governs its operation: **Planning \-\> Reasoning \-\> Taking Actions \-\> Evaluating Results**.6 This loop is not an abstract concept but the tangible process embodied by Kiro's spec-driven workflow. It represents a deliberate departure from the direct code generation model of other tools, instead forcing a structured approach that mirrors formal software engineering practices.

The loop begins when a developer provides a high-level goal. The agent then proceeds through its phases:

1. **Planning & Reasoning:** This phase is where Kiro translates a developer's abstract intent into a concrete, verifiable plan. Given a prompt like "Make me a Task Management app" or "Add a review system for products," the agent does not immediately write code.1 Instead, it engages in a planning process, analyzing the request and the existing codebase to generate the initial specification documents:  
   requirements.md and design.md.9 This stage is designed to unpack assumptions, clarify ambiguities, and formulate a comprehensive technical blueprint before a single line of implementation code is written.  
2. **Taking Actions:** Once the human developer has reviewed and approved the specification documents, the agent moves to execution. This phase is guided by the tasks.md file, which contains a granular, step-by-step checklist derived from the design document.1 The agent's actions are precise and targeted; it will open relevant files, make the required modifications, and create new files as dictated by the plan, enabling true end-to-end feature development across the project.6  
3. **Evaluating Results:** Kiro demonstrates a capacity for reasoning that extends beyond simple task execution. After taking an action, it can observe the outcome. For instance, it can recognize a compiler error reported in the terminal. Critically, it can then reason about this error within the context of the overall plan. In one documented case, the agent correctly identified that a minor compiler issue would be resolved by a future task in its queue and consciously chose to defer the fix, preventing it from deviating from the approved plan.5 This ability to evaluate results and make context-aware decisions is a hallmark of a truly agentic system.

This entire process is designed to be the bridge from a loosely defined idea—the "vibe"—to production-ready, "viable" code.3 By creating "living documentation" in the form of spec files that evolve alongside the code, Kiro ensures that the project remains understandable, maintainable, and aligned with its original goals throughout the development lifecycle.10 The user experience is consequently more structured than a free-form chat. A developer initiates a "Spec" session, provides a feature description, and is then guided through a phased workflow of reviewing and approving the Requirements, then the Design, and finally overseeing the Implementation.10

This structured workflow serves a deeper purpose than just project management. Standard interactions with large language models (LLMs) often feel like a "black box"; the user provides a prompt and receives an output, but the model's internal reasoning process remains hidden.13 This opacity can lead to problems, as LLMs can misinterpret ambiguous instructions or "forget" critical context during long, complex sessions.14 Kiro's methodology directly mitigates these weaknesses by externalizing the AI's "thought process" for human oversight. The generation of

requirements.md forces the AI to first articulate its *understanding* of the user's request. The subsequent creation of design.md and tasks.md compels it to document its *plan* for implementation.1 The crucial step is that the developer is prompted to review, edit, and approve these documents

*before* the agent begins coding.5 In this model, the spec files are not merely documentation; they are cognitive artifacts. They function as the AI's externalized working memory and plan of action, making its reasoning process transparent, editable, and verifiable. This transforms the human-AI interaction from one of simple instruction to one of strategic collaboration and architectural review, placing the human firmly in the role of technical lead.

## **Section 2: The Project Blueprint: A Granular Analysis of Kiro's Spec Files**

The spec-driven development process in Kiro revolves around a core set of three markdown files: requirements.md, design.md, and tasks.md. These files are generated as a cohesive set for each new feature or significant change, serving as the "single source of truth" for that unit of work.10 This modular approach—for example, having one set of specs for user authentication and another for a product catalog—makes large projects more manageable and facilitates easier collaboration.15 These artifacts are the tangible output of the agent's planning phase and the primary interface for developer oversight and approval.

The following table provides a high-level overview of Kiro's complete markdown file ecosystem, illustrating the distinct roles of the per-feature spec files and the project-wide steering files.

**Table 2: The Kiro Markdown File Ecosystem**

| File Name | Location | Purpose | Core Question Answered |
| :---- | :---- | :---- | :---- |
| requirements.md | Per-feature (e.g., specs/auth/) | Defines user stories and acceptance criteria | "WHAT should be built?" |
| design.md | Per-feature | Outlines technical architecture and components | "HOW should it be built?" |
| tasks.md | Per-feature | Provides a step-by-step implementation checklist | "WHAT are the exact steps to build it?" |
| product.md | .kiro/steering/ | Defines product vision and goals | "WHY are we building this project?" |
| tech.md | .kiro/steering/ | Documents the technology stack | "WITH WHAT tools will we build it?" |
| structure.md | .kiro/steering/ | Defines file organization and conventions | "WHERE does the code go?" |
| \[custom\].md | .kiro/steering/ | Defines team-specific rules (e.g., API standards) | "WHAT are our specific rules?" |

### **2.1. requirements.md: Defining the "What" with Unambiguous Precision**

The requirements.md file is the foundational artifact in the Kiro workflow. It is the first document generated by the agent after receiving the developer's high-level feature description.1 Its primary purpose is to deconstruct the initial, often informal, prompt into a set of structured user stories, each accompanied by detailed acceptance criteria.9 This process is designed to make all of the AI's initial assumptions explicit, allowing the developer to verify that the agent is aligned with the intended goal before any further planning or coding occurs.9

The structure typically consists of several user stories, with each story containing four to six acceptance criteria that cover core functionality, edge cases, and error conditions.1 The most critical and innovative aspect of this file is its mandated use of the

**Easy Approach to Requirements Syntax (EARS)**.9 EARS is a controlled natural language—a set of simple, structured templates—designed specifically to reduce or eliminate the ambiguity, inconsistency, and vagueness inherent in unconstrained natural language.16 This is particularly vital when communicating with LLMs, which are highly susceptible to misinterpretation when faced with imprecise instructions.

The EARS methodology provides a small number of patterns, each identified by a specific keyword, to frame requirements clearly. The generic syntax follows a logical, temporal order: While \<optional pre-condition\>, when \<optional trigger\>, the \<system name\> shall \<system response\>.17 This structure ensures that every requirement is clear, testable, and complete.

The adoption of EARS within Kiro is a profound design choice. While effective communication between any two systems requires a well-defined contract or schema, the communication between a human and an AI agent has historically relied on the "schemaless" protocol of natural language. This ambiguity is a primary source of error and frustration. Kiro's use of EARS effectively imposes a strict, predictable structure on this communication. The keywords (When, While, If, Where) and the fixed order of clauses function like the fields in a well-defined API payload. This transforms the act of writing requirements from simple prompting into a more rigorous act of programming the agent's understanding. EARS serves as the API schema for translating high-level human intent into a machine-interpretable format that dramatically reduces the probability of the agent misunderstanding the "request."

The following table details the primary EARS patterns used within Kiro's requirements.md files, providing a practical guide to their syntax and application.

**Table 3: EARS Requirement Patterns and Syntax**

| Pattern Name | Description | EARS Keywords | Example |
| :---- | :---- | :---- | :---- |
| **Ubiquitous** | A universal requirement, always true. Defines a fundamental system property. | The \<system\> shall... | "The system shall be written in Python." 18 |
| **Event-Driven** | A response to a specific, discrete trigger event. | When \<trigger\>, the \<system\> shall... | "When the user clicks the 'Submit' button, the system shall save the form data." 19 |
| **State-Driven** | Active only while the system is in a specific, continuous state. | While \<state\>, the \<system\> shall... | "While the system is processing the payment, the system shall display a loading icon." 19 |
| **Optional Feature** | Applies only if a specific, optional feature is present in the system. | Where \<feature\>, the \<system\> shall... | "Where the car has a sunroof, the car shall have a sunroof control panel." 17 |
| **Unwanted Behavior** | Specifies the required system response to an undesirable situation or error. | If \<condition\>, then the \<system\> shall... | "If an invalid credit card number is entered, then the website shall display an error message." 17 |

### **2.2. design.md: Architecting the "How" as the Technical Source of Truth**

Following the developer's approval of the requirements.md file, Kiro proceeds to the next phase of planning: generating the design.md document. This file serves as the comprehensive technical blueprint for the feature, translating the "what" from the requirements into a detailed plan for "how" it will be built.1 The agent creates this document by analyzing the now-approved requirements in conjunction with the existing codebase and the project-wide rules defined in the steering files.9

The design.md file is the "source of truth" for the technical implementation.1 Its contents are rich and varied, designed to provide a complete architectural picture before coding begins. A typical

design.md generated by Kiro includes:

* **Component and Feature Lists:** A breakdown of the new components, modules, or services that will be created.  
* **Data Models and Database Schemas:** Detailed definitions for new or modified data structures, often including database schema definitions for tools like Prisma.8  
* **Type Definitions and Interfaces:** For statically-typed languages like TypeScript, Kiro generates the necessary type and interface definitions to ensure data consistency.8  
* **API Specifications:** Formal definitions for any new API endpoints, which can include RESTful conventions or even OpenAPI specifications.8  
* **Error Handling and Testing Strategies:** Outlines for how errors will be managed and what unit or integration tests will be required.1

A standout feature of the design.md is Kiro's ability to generate visualizations directly within the document. Using the simple, text-based Mermaid syntax, the agent can create data flow diagrams, sequence diagrams, and architectural charts.5 This provides an invaluable visual representation of the proposed architecture, making complex interactions and data flows much easier for the developer to understand, review, and validate.

### **2.3. tasks.md: The Actionable "To-Do" List for Agentic Execution**

The final artifact in the spec trio is tasks.md. This file is the bridge between planning and execution. It is generated from the design.md and deconstructs the high-level architectural plan into a granular, dependency-aware checklist of discrete coding tasks.1 Its purpose is to provide a clear, step-by-step implementation plan that can be executed and tracked, ensuring a controlled and methodical development process.1

The structure of tasks.md is designed for clarity and traceability. Each major task is explicitly linked back to the specific requirements and acceptance criteria from requirements.md that it helps fulfill.5 This ensures that no part of the original request is overlooked during implementation. Furthermore, Kiro often breaks down these major tasks into detailed sub-tasks, which can include specific implementation details such as:

* Writing unit tests for a new function.  
* Implementing integration tests between components.  
* Adding loading states for asynchronous operations.  
* Ensuring mobile responsiveness and accessibility standards are met.9

This level of detail transforms the tasks.md from a simple to-do list into a comprehensive execution script for the agent. The developer interacts with this file by selecting tasks, often one by one, for the agent to execute.13 This phased execution allows for incremental development, testing, and verification, giving the developer fine-grained control over the agent's progress and the ability to intervene or make corrections at any step.1

## **Section 3: The Agent's Memory: Mastering Context with Steering Files**

One of the most significant challenges in leveraging LLMs for complex, multi-turn tasks is the management of context. Models have finite context windows, and providing consistent, project-wide instructions across every interaction is inefficient and prone to error. Kiro's solution to this fundamental problem is a system of **Steering Files**. These are persistent markdown documents that provide the AI agent with a permanent "memory" of the project's specific rules, conventions, technologies, and goals.21

These crucial files reside in a dedicated .kiro/steering/ directory at the root of the project.7 They are typically created by running the

Kiro: Setup Steering for Project command from the command palette, which generates a default set of three files.10 Unless configured otherwise, the contents of these files are automatically included as high-priority context in every interaction the developer has with the Kiro agent, ensuring that its behavior is always aligned with the project's established standards.21

### **3.1. The Core Steering Trio: product.md, tech.md, and structure.md**

Kiro establishes a baseline of project understanding through three foundational steering files, each answering a critical question about the project's nature.

* **product.md (The "Why"):** This file defines the high-level vision of the application. It contains information about the product's core purpose, its target users or platforms, its key features, and its overarching business objectives.1 By understanding the "why" behind the project, the agent can make more intelligent decisions, suggesting solutions and new features that align with the product's strategic goals rather than just fulfilling a narrow technical request.  
* **tech.md (The "With What"):** This document serves as the definitive record of the project's technology stack. It lists the chosen programming languages, frameworks (e.g., React, Node.js), key libraries and dependencies, development tools, and common commands (e.g., npm test).1 This file is essential for maintaining technical consistency. It guides the agent to use the correct tech stack, preventing it from introducing extraneous or incompatible technologies, and enables it to autonomously execute commands for testing, building, or linting the codebase.  
* **structure.md (The "Where"):** This file outlines the project's organizational and architectural conventions. It details the file and folder structure, specifies naming conventions for components and variables, and documents key architectural principles (e.g., "all state management logic resides in the src/store directory").1 This context is vital for the agent's ability to navigate the codebase and generate new code that fits seamlessly into the existing structure, maintaining a clean and consistent project architecture.

### **3.2. Advanced Steering: Customization and Dynamic Context**

The steering system is not limited to the default trio. Its true power lies in its extensibility and its sophisticated mechanisms for dynamic context management. Developers can create any number of **custom steering files** to codify team-specific or domain-specific knowledge. For example, a team might create api-standards.md to enforce RESTful conventions, testing-patterns.md to define unit testing approaches, or security-checklist.md to outline security best practices.21

To prevent context windows from becoming bloated with irrelevant information, Kiro implements a powerful **inclusion logic** system controlled by YAML front matter at the top of each steering file.21 This allows for fine-grained control over when a given file's content is provided to the agent.

This system of steering and spec files creates a sophisticated, hierarchical context model. It moves far beyond the common prompt engineering technique of providing a flat, undifferentiated blob of information. At the top of the hierarchy are the steering files, which represent the global, persistent context—the project's "constitution." Below this is the local, feature-level context provided by the spec files—the specific "bill" being debated for the current task. The agent is designed to process this hierarchy, applying the global rules from steering to the specific instructions found in the specs.7 The inclusion modes (

always, conditional, manual) add a further layer of dynamic filtering, ensuring that the context provided to the LLM is not only hierarchical but also maximally relevant and minimally verbose. This entire system mimics the cognitive process of an expert human developer, who recalls general principles and patterns and applies them to the specific problem at hand.

The following table outlines the different inclusion modes, which are critical for managing context size, relevance, performance, and cost.

**Table 4: Steering File Inclusion Modes**

| Inclusion Mode | YAML Syntax | Use Case | Best For |
| :---- | :---- | :---- | :---- |
| **Always Included (Default)** | (No YAML needed) or \--- inclusion: always \--- | The file's content is included in every agent interaction. | Universal standards like the core technology stack, project-wide coding conventions, and fundamental security policies.21 |
| **Conditional Inclusion** | \--- inclusion: conditional patterns: \["\*.tsx", "app/api/\*\*/\*"\] \--- | The file's content is included only when files matching the glob pattern are part of the active context. | Domain-specific rules, such as React component patterns, API design guidelines for backend routes, or documentation standards for markdown files.21 |
| **Manual Inclusion** | \--- inclusion: manual \--- | The file's content is included only when explicitly referenced in a chat prompt using \#steering-file-name. | Specialized, occasional-use documents like troubleshooting guides, complex data migration procedures, or onboarding instructions.21 |

To further combat documentation drift and ensure that steering rules remain current, the system supports **dynamic file references**. Using the syntax \#\[\[file:\<relative\_path\_to\_file\>\]\], a steering file can embed a live reference to a source code file.21 For example,

structure.md could reference a key configuration file like vite.config.ts to ensure the agent always has the latest build configuration. This turns the steering documents from static text into a living system that is dynamically linked to the state of the codebase itself.

## **Section 4: The Extended Ecosystem: Automation and Extensibility**

Beyond the core spec-driven planning and context steering systems, Kiro is equipped with an extended ecosystem of features that elevate it from a sophisticated code generator to a true agentic Integrated Development Environment (IDE). Two key components of this ecosystem are Agent Hooks and the Model Context Protocol (MCP), which provide powerful automation and extensibility capabilities.

### **4.1. Agent Hooks: Intelligent Automation for the Development Lifecycle**

**Agent Hooks** are event-driven automation triggers that delegate repetitive or boilerplate tasks to an AI agent, allowing it to work quietly in the background while the developer remains focused on creative problem-solving.1 The concept is analogous to serverless functions triggered by cloud events: "Do X when Y happens".1 Hooks are configured not with code, but by describing the desired automation in natural language within the Kiro interface.22

The system supports several types of triggers for these automations:

* **File Created**  
* **File Saved**  
* **File Deleted**  
* **Manual Trigger** (invoked from the command palette) 22

These triggers can be combined with file path patterns (e.g., src/components/\*\*/\*.tsx) to create highly specific and useful automations.22 Agent Hooks are particularly effective for enforcing team-wide consistency and improving code quality across a project. Practical applications include:

* **Automated Test Generation:** A hook can be configured so that whenever a developer saves a React component file, an agent automatically creates or updates its corresponding test file (e.g., MyComponent.test.tsx), scaffolding out the necessary tests.9  
* **Living Documentation:** A hook can monitor changes to API endpoint files and automatically refresh the project's README.md or other documentation to reflect the latest API signatures.9  
* **Automated Quality & Security Checks:** A hook can be set up as a manual trigger or tied to a pre-commit action to have an agent scan for leaked credentials, check for adherence to coding standards, or lint the codebase.9

By embedding these quality checks directly into the development workflow, Agent Hooks help prevent issues from escalating and ensure that standards are applied consistently by every team member.9

### **4.2. Model Context Protocol (MCP): Extending Kiro's Knowledge Base**

The **Model Context Protocol (MCP)** is Kiro's mechanism for extending its capabilities beyond the knowledge inherent in its underlying LLM. MCP allows Kiro to connect to and utilize external tools, APIs, databases, and specialized data sources, effectively giving the agent access to real-time, domain-specific information.6

MCP servers are configured via a central JSON file within the Kiro environment. In this file, a developer can enable or disable pre-packaged servers (like a web fetch utility) or add new, custom servers by specifying the command needed to run them and any required environment variables, such as API keys.22 For example, a developer could configure an MCP server that provides access to the Brave Search API to give Kiro real-time web search capabilities.22

Once configured, these external tools can be leveraged in several ways:

* **Direct Questions:** The developer can ask questions in the chat that implicitly require external knowledge (e.g., "Search for the latest best practices for React 18"), and Kiro will use the appropriate MCP server to find the answer.22  
* **Explicit Tool Usage:** Tools can be invoked explicitly using the \#mcp or tool-specific context providers in the chat, such as \#\[fetch\] Use the web search to find examples of TypeScript generic constraints.22  
* **Integration with Other Features:** MCP can be combined with other Kiro features. For instance, an Agent Hook could be created that uses a web search MCP to find and include relevant documentation links whenever a new component file is created.22

MCP is a critical feature that allows Kiro to overcome the static knowledge limitations of LLMs, enabling it to reason with up-to-date information and interact with a wide range of external systems.

## **Section 5: Implementation Guide: Adapting the Kiro Logic for Custom Cursor Modes**

This section provides a practical, strategic blueprint for translating the architectural principles of Kiro into an enhanced set of custom modes within the Cursor IDE. The goal is to simulate Kiro's structured, spec-driven workflow by leveraging Cursor's capabilities for file I/O and sophisticated prompting. This implementation adopts a tool-agnostic folder structure that mirrors Kiro's conventions, allowing for seamless interoperability. This means you can use symbolic links (ln \-s) to point Cursor's .cursor-rules/ directory to the tool-agnostic .ai-rules/ folder, enabling both IDEs to work from a single source of truth without modification.

### **5.1. A Tool-Agnostic Architecture for Interoperability**

To ensure you can switch between Kiro and your custom Cursor modes without friction, we will adopt a neutral, centralized folder structure for all AI-related artifacts.

#### **The .ai-rules/ and specs/ Directories**

At the root of your project, establish two key directories:

* **.ai-rules/**: This directory will serve as the single source of truth for persistent, project-wide context. It will house the core steering files, named according to Kiro's convention:  
  * product.md  
  * tech.md  
  * structure.md  
  * Any custom rule files (e.g., api-conventions.md, testing-patterns.md).  
* **specs/**: This directory will house the specifications for each feature, with each feature getting its own dedicated subfolder. This modular approach is key to managing complexity.15 For example:  
  * specs/user-authentication/  
  * specs/product-catalog/

To make this work in both IDEs, you would create symbolic links:

* In Kiro, the .kiro/steering directory would link to the root .ai-rules/ directory.  
* In Cursor, the .cursor/rules directory would link to the root .ai-rules/ directory.  
* Both IDEs would work directly with the root specs/ directory.

### **5.2. The Interactive "Planner" Mode: Collaborative Specification**

The "Planner" mode is reimagined as an interactive, multi-step dialogue between the developer and the AI. This collaborative process ensures alignment and allows for course correction before any code is written, directly engaging the developer in key requirement and design decisions.

The workflow proceeds as follows:

1. **Feature Scoping and Naming:** The process begins with the developer providing a high-level feature description. The Planner's first action is to ask for a concise, machine-friendly name for the feature (e.g., "user-auth," "product-reviews"). This name is then used to create the dedicated spec subdirectory (e.g., specs/user-auth/), answering the question of how the agent knows where to place the spec files.24  
2. **Iterative Requirement Definition:** The Planner generates a first draft of requirements.md within the new spec folder. Crucially, it does not stop here. It presents the generated user stories and EARS-based acceptance criteria to the developer and asks for feedback. It might pose clarifying questions like, "I've assumed that users must verify their email to log in. Is this correct?" or "Should we consider a 'remember me' functionality?." This loop continues until the developer approves the requirements.  
3. **Collaborative Technical Design:** Once the requirements are finalized, the Planner generates the design.md file. If the agent identifies multiple viable architectural paths based on the project's tech.md and the new requirements, it will present these options to the developer. For example: "For state management, we could use the existing Redux setup or introduce Zustand for this feature, which might be simpler. Pros of Redux are... Cons are... Which approach do you prefer?" This step ensures the developer retains architectural control.  
4. **Final Task Generation:** With the design approved, the Planner generates the final tasks.md file, breaking down the agreed-upon design into a granular, actionable checklist.

### **5.3. The Focused "Executive" Mode: Plan-Driven Implementation**

The "Executive" mode is streamlined to be a pure executor of the plan created by the interactive Planner. Its role is to methodically work through the tasks.md file, ensuring the implementation adheres strictly to the approved specification.

* **Input:** The path to a specific tasks.md file (e.g., specs/user-auth/tasks.md).  
* **Process:** The Executive mode's prompt instructs the AI to:  
  1. **Ingest All Context:** Read the complete local context from the requirements.md, design.md, and tasks.md files in the specified feature directory, as well as the global context from all files in .ai-rules/.  
  2. **Execute a Single Task:** Identify the first incomplete task in tasks.md, implement the necessary code changes across the project, and strictly follow all design and steering conventions.  
  3. **Update and Persist State:** After successfully completing the task, the agent must edit the tasks.md file to mark the task as complete (e.g., changing \[ \] to \[x\]). This creates a persistent record of progress and ensures the next run of the Executive will pick up the subsequent task.  
* **Output:** Modified source code files and the updated tasks.md file.

### **5.4. Advanced Prompting for the Simulated Workflow**

The success of this simulation hinges on master prompts that blend the intelligence of your original prompts with the structured, interactive methodology of Kiro.

#### **The "Planner" Master Prompt Template (Interactive Mode)**

This prompt establishes the AI as a collaborative partner, guiding it through the interactive planning session.

# **ROLE: Expert AI Software Architect & Collaborative Planner**

# **PREAMBLE:**

This session synthesizes the strategic planning capabilities of your original Planner mode with the rigorous, spec-driven methodology of Kiro. Your primary goal is to collaborate with the user to define a feature, not just to generate files. You must be interactive, ask clarifying questions, and present alternatives when appropriate.

# **CONTEXT:**

You MUST operate within the project's established standards, defined in the following global context files. You will read and internalize these before beginning.

* Product Vision: @.ai-rules/product.md  
* Technology Stack: @.ai-rules/tech.md  
* Project Structure & Conventions: @.ai-rules/structure.md  
* (Load any other custom.md files from.ai-rules/ as well)

# **WORKFLOW:**

You will guide the user through a three-phase interactive process: Requirements, Design, and Tasks. Do NOT proceed to the next phase until the user has explicitly approved the current one.

## **Phase 1: Requirements Definition (Interactive Loop)**

1. **Initiate:** Start by greeting the user and acknowledging their feature request: {{user\_request}}.  
2. **Name the Spec:** Ask the user for a short, kebab-case name for this feature (e.g., "user-authentication"). This name will be used for the spec directory. Wait for their response. Once provided, confirm the creation of the directory: specs/{{feature\_name}}/.  
3. **Generate Draft:** Create a draft of requirements.md in the new directory. Decompose the user's request into user stories with detailed acceptance criteria. ALL acceptance criteria MUST strictly follow the Easy Approach to Requirements Syntax (EARS).  
4. **Review and Refine:** Present the draft to the user. Ask specific, clarifying questions to resolve ambiguities (e.g., "I've included a requirement for password complexity. What are the specific rules?"). If there are common alternative paths, present them (e.g., "Should users be able to sign up with social accounts as well?").  
5. **Finalize:** Once the user agrees, save the final requirements.md and state that the requirements phase is complete. Ask for confirmation to proceed to the Design phase.

## **Phase 2: Technical Design (Interactive Loop)**

1. **Generate Draft:** Based on the approved requirements.md and the global context, generate a draft of design.md. This must be a complete technical blueprint, including Data Models, API Endpoints, Component Structure, and Mermaid diagrams for visualization.  
2. **Identify and Present Choices:** Analyze the design for key architectural decisions. If alternatives exist (e.g., different libraries for a specific task, different data-fetching patterns), present them to the user with a brief list of pros and cons for each. Ask the user to make a choice.  
3. **Review and Refine:** Present the full design draft for user review. Incorporate their feedback.  
4. **Finalize:** Once the user approves the design, save the final design.md. State that the design phase is complete and ask for confirmation to proceed to the Task generation phase.

## **Phase 3: Task Generation (Final Step)**

1. **Generate Tasks:** Based on the approved design.md, generate the tasks.md file. Break down the implementation into a granular, dependency-aware checklist of actionable tasks.  
2. **Conclude:** Announce that the planning is complete and the tasks.md file is ready for the Executive mode.

# **OUTPUT:**

Throughout the interaction, provide clear instructions and present the file contents for review. The final output of this entire mode is the set of three files in specs/{{feature\_name}}/.

#### **The "Executive" Master Prompt Template**

This prompt is focused on precise, single-task execution based on the comprehensive plan.

# **ROLE: Meticulous AI Software Engineer**

# **PREAMBLE:**

This mode synthesizes the robust execution logic of your original Executive prompt with Kiro's principle of plan-adherence. Your focus is surgical precision. You will execute ONE task and only one task.

# **CONTEXT:**

You are implementing a single task from a pre-approved plan. You MUST operate within the full context of the project's rules and the feature's specific plan.

## **Feature-Specific Context (The Plan):**

* Requirements: @specs/{{feature\_name}}/requirements.md  
* Technical Design: @specs/{{feature\_name}}/design.md  
* Task List: @specs/{{feature\_name}}/tasks.md

## **Global Project Context (The Rules):**

* Product Vision: @.ai-rules/product.md  
* Technology Stack: @.ai-rules/tech.md  
* Project Structure & Conventions: @.ai-rules/structure.md  
* (Load any other custom.md files from.ai-rules/ as well)

# **TASK:**

Your goal is to execute the NEXT incomplete task from the tasks.md file and then stop.

# **INSTRUCTIONS:**

1. **Identify Task:** Scan tasks.md and identify the very first task that is not marked as complete (\[ \]).  
2. **Understand Task:** Read the task description. Refer to design.md and requirements.md to fully understand the technical details and the user-facing goal of this task.  
3. **Implement Changes:** Apply the necessary code changes to any files in the project to complete this single task. You MUST strictly adhere to all conventions defined in the Global and Feature-Specific context files.  
4. **Update State:** After applying the code changes, you MUST modify the tasks.md file by changing the checkbox for the completed task from \[ \] to \[x\]. This is a critical step.

# **OUTPUT FORMAT:**

Provide the file diffs for all source code changes AND the complete, updated content of the tasks.md file.

### **5.5. Acknowledging the "Real-World" Challenges**

Based on early user experiences with Kiro, it is prudent to anticipate and mitigate potential challenges when implementing this workflow.

* **Performance and Timeouts:** The Kiro workflow, with its multi-step analysis and generation, is inherently slower than a single-shot prompt.13 This simulation in Cursor will likely exhibit similar performance characteristics. For very large or complex features, it is advisable to break them down into smaller, more manageable specs to avoid hitting model context limits or experiencing long wait times.  
* **Over-engineering and Code Quality:** Users have reported that Kiro can sometimes produce overly complex, convoluted, or messy code.13 The human developer's role as a quality gate is paramount. The interactive nature of the new Planner mode is the key control point. Before approving the design, the developer should meticulously review the generated  
  design.md, simplifying the architecture and refining the approach where necessary. The goal is to guide the AI toward an elegant solution, not to blindly accept its first proposal.  
* **The Rigidity Trade-off:** The structured Kiro methodology is not a panacea for all development tasks. Its overhead is best justified for new feature development, complex refactoring, or building substantial modules where upfront planning provides a clear return on investment. It is recommended to maintain the original, more flexible custom modes for smaller tasks like quick bug fixes, simple refactors, or rapid, exploratory prototyping. The developer should choose the right tool—the flexible prompt or the structured spec—for the job at hand.

## **Conclusion: The Future of Development – Structured, Agentic, and Verifiable**

The analysis of Kiro reveals that its true innovation lies not in any single feature, but in its cohesive, opinionated methodology that brings architectural rigor to AI-driven software development. It champions a paradigm shift away from the ephemeral, conversational nature of "vibe coding" toward a more durable and deliberate process. The core principles underpinning this shift are **externalized planning**, **persistent memory**, and **structured communication**.

1. **Externalized Planning:** By forcing the agent to generate and seek approval for requirements.md, design.md, and tasks.md before writing code, Kiro makes the AI's reasoning process transparent and verifiable. It externalizes the "thought process" into editable artifacts, transforming the developer's role from a mere prompter to an architect and reviewer.  
2. **Persistent Memory:** Through the use of steering files, Kiro solves the critical problem of long-term context. It provides the agent with a permanent, hierarchical understanding of the project's goals, technologies, and conventions, ensuring consistent and aligned behavior across all interactions.  
3. **Structured Communication:** The mandated use of the EARS syntax is a masterstroke in human-agent interaction design. It replaces the ambiguity of unconstrained natural language with a clear, schematized protocol, effectively creating an "API" for human intent that dramatically reduces the risk of misinterpretation by the LLM.

By adopting these principles, even in a simulated fashion within a tool like Cursor, a developer can build a system that moves beyond the "prompt-and-pray" cycle.25 The implementation of a file-based spec and steering system can lead to the generation of more consistent, maintainable, and well-documented code. This structured approach provides the guardrails necessary to build robust and scalable applications with AI assistance, mitigating the risks of creating unmanageable "vibe-coded" systems.

Ultimately, Kiro represents a significant and logical step toward a future of autonomous software engineering. It paints a picture of a development process where humans act less as line-by-line coders and more as strategic architects, guiding intelligent, autonomous agents through well-defined specifications. The techniques and architectural patterns deconstructed in this report provide a practical pathway for any developer looking to begin operating in this emerging paradigm today.

#### **Works cited**

1. Kiro just unlocked the secret to vibe coding — and it's wildly effective ..., accessed on July 18, 2025, [https://medium.com/@dpkmos/kiro-just-unlocked-the-secret-to-vibe-coding-and-its-wildly-effective-12346278d4cf](https://medium.com/@dpkmos/kiro-just-unlocked-the-secret-to-vibe-coding-and-its-wildly-effective-12346278d4cf)  
2. Kiro.dev \- The AI IDE for prototype to production | Hacker News, accessed on July 18, 2025, [https://news.ycombinator.com/item?id=44561303](https://news.ycombinator.com/item?id=44561303)  
3. Amazon targets vibe-coding chaos with new 'Kiro' AI software development tool \- GeekWire, accessed on July 18, 2025, [https://www.geekwire.com/2025/amazon-targets-vibe-coding-chaos-with-new-kiro-ai-software-development-tool/](https://www.geekwire.com/2025/amazon-targets-vibe-coding-chaos-with-new-kiro-ai-software-development-tool/)  
4. Kiro: A new agentic IDE | Hacker News, accessed on July 18, 2025, [https://news.ycombinator.com/item?id=44560662](https://news.ycombinator.com/item?id=44560662)  
5. Cognition (Devin AI) to Acquire Windsurf | Hacker News, accessed on July 18, 2025, [https://news.ycombinator.com/item?id=44563324](https://news.ycombinator.com/item?id=44563324)  
6. Introducing Kiro – An AI IDE That Thinks Like a Developer \- DEV Community, accessed on July 18, 2025, [https://dev.to/aws-builders/introducing-kiro-an-ai-ide-that-thinks-like-a-developer-42jp](https://dev.to/aws-builders/introducing-kiro-an-ai-ide-that-thinks-like-a-developer-42jp)  
7. AWS Kiro: Another AI-Powered IDE Challenger or a Game Changer? \- DEV Community, accessed on July 18, 2025, [https://dev.to/onepoint/aws-kiro-another-ai-powered-ide-challenger-or-a-game-changer-1bj8](https://dev.to/onepoint/aws-kiro-another-ai-powered-ide-challenger-or-a-game-changer-1bj8)  
8. Kiro Dev vs Cursor vs Github Copilot \- Reddit, accessed on July 18, 2025, [https://www.reddit.com/r/cursor/comments/1m2reyz/kiro\_dev\_vs\_cursor\_vs\_github\_copilot/](https://www.reddit.com/r/cursor/comments/1m2reyz/kiro_dev_vs_cursor_vs_github_copilot/)  
9. Introducing Kiro \- Kiro.dev, accessed on July 18, 2025, [https://kiro.dev/blog/introducing-kiro/](https://kiro.dev/blog/introducing-kiro/)  
10. Kiro Agentic AI IDE: Beyond a Coding Assistant \- Full Stack Software Development with Spec Driven AI | AWS re:Post, accessed on July 18, 2025, [https://repost.aws/articles/AROjWKtr5RTjy6T2HbFJD\_Mw/%F0%9F%91%BB-kiro-agentic-ai-ide-beyond-a-coding-assistant-full-stack-software-development-with-spec-driven-ai](https://repost.aws/articles/AROjWKtr5RTjy6T2HbFJD_Mw/%F0%9F%91%BB-kiro-agentic-ai-ide-beyond-a-coding-assistant-full-stack-software-development-with-spec-driven-ai)  
11. Amazon's new Claude-powered spec-driven IDE (Kiro) feels like a game-changer. Thoughts? : r/ClaudeAI \- Reddit, accessed on July 18, 2025, [https://www.reddit.com/r/ClaudeAI/comments/1lzsvot/amazons\_new\_claudepowered\_specdriven\_ide\_kiro/](https://www.reddit.com/r/ClaudeAI/comments/1lzsvot/amazons_new_claudepowered_specdriven_ide_kiro/)  
12. Specs \- Docs \- Kiro \- Kiro.dev, accessed on July 18, 2025, [https://kiro.dev/docs/specs/](https://kiro.dev/docs/specs/)  
13. Amazon's Cursor Competitor Kiro is Surprisingly good\!\! \- Reddit, accessed on July 18, 2025, [https://www.reddit.com/r/cursor/comments/1m0eusx/amazons\_cursor\_competitor\_kiro\_is\_surprisingly/](https://www.reddit.com/r/cursor/comments/1m0eusx/amazons_cursor_competitor_kiro_is_surprisingly/)  
14. I tried Kiro the coffee assistant from Amazon with my svelte project, you won't believe it : r/sveltejs \- Reddit, accessed on July 18, 2025, [https://www.reddit.com/r/sveltejs/comments/1m0r67e/i\_tried\_kiro\_the\_coffee\_assistant\_from\_amazon/](https://www.reddit.com/r/sveltejs/comments/1m0r67e/i_tried_kiro_the_coffee_assistant_from_amazon/)  
15. Hands on with Kiro, the AWS preview of an agentic AI IDE driven by specifications \- devclass, accessed on July 18, 2025, [https://devclass.com/2025/07/15/hands-on-with-kiro-the-aws-preview-of-an-agentic-ai-ide-driven-by-specifications/](https://devclass.com/2025/07/15/hands-on-with-kiro-the-aws-preview-of-an-agentic-ai-ide-driven-by-specifications/)  
16. Easy Approach to Requirements Syntax (EARS) : r/ReqsEngineering \- Reddit, accessed on July 18, 2025, [https://www.reddit.com/r/ReqsEngineering/comments/1hept25/easy\_approach\_to\_requirements\_syntax\_ears/](https://www.reddit.com/r/ReqsEngineering/comments/1hept25/easy_approach_to_requirements_syntax_ears/)  
17. EARS \- Alistair Mavin, accessed on July 18, 2025, [https://alistairmavin.com/ears/](https://alistairmavin.com/ears/)  
18. EARS: The Easy Approach to Requirements Syntax \- DEV Community, accessed on July 18, 2025, [https://dev.to/sebastian\_dingler/ears-the-easy-approach-to-requirements-syntax-39a5](https://dev.to/sebastian_dingler/ears-the-easy-approach-to-requirements-syntax-39a5)  
19. Listen Up\! How EARS Can Transform Your User Stories \- theBAlab, accessed on July 18, 2025, [https://www.thebalab.com/post/listen-up-how-ears-can-transform-your-user-stories?utm\_source=linkedin\&utm\_medium=social-marketing\&utm\_campaign=10a64bc4-54f7-438e-a876-e619bfcbbc2f](https://www.thebalab.com/post/listen-up-how-ears-can-transform-your-user-stories?utm_source=linkedin&utm_medium=social-marketing&utm_campaign=10a64bc4-54f7-438e-a876-e619bfcbbc2f)  
20. Kiro \- updated review : r/webdev \- Reddit, accessed on July 18, 2025, [https://www.reddit.com/r/webdev/comments/1m1v4ic/kiro\_updated\_review/](https://www.reddit.com/r/webdev/comments/1m1v4ic/kiro_updated_review/)  
21. Steering \- Docs \- Kiro \- Kiro.dev, accessed on July 18, 2025, [https://kiro.dev/docs/steering/](https://kiro.dev/docs/steering/)  
22. Your First Project \- Docs \- Kiro \- Kiro.dev, accessed on July 18, 2025, [https://kiro.dev/docs/getting-started/first-project/](https://kiro.dev/docs/getting-started/first-project/)  
23. Get started \- Docs \- Kiro.dev, accessed on July 18, 2025, [https://kiro.dev/docs/getting-started/](https://kiro.dev/docs/getting-started/)  
24. Best practices \- Docs \- Kiro.dev, accessed on July 18, 2025, [https://kiro.dev/docs/specs/best-practices/](https://kiro.dev/docs/specs/best-practices/)  
25. Amazon just launched Kiro.dev. An AI IDE for Spec-Driven Development (It's amazing\!) : r/programming \- Reddit, accessed on July 18, 2025, [https://www.reddit.com/r/programming/comments/1m1xxwc/amazon\_just\_launched\_kirodev\_an\_ai\_ide\_for/](https://www.reddit.com/r/programming/comments/1m1xxwc/amazon_just_launched_kirodev_an_ai_ide_for/)