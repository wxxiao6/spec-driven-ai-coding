# Kiro-style Prompts for Spec-Driven Development

This project provides a set of prompts for Cursor to implement a structured, spec-driven "Plan & Execute" workflow, inspired by the principles of AWS Kiro. It's designed to move beyond reactive "vibe coding" towards a proactive process that produces well-documented, maintainable, and production-ready code.

The primary motivation behind this methodology is to enable a consistent, spec-driven development process across any AI coding assistant. By standardizing the project's rules and specifications, you can seamlessly switch between tools like Kiro, Cursor, Claude, or Gemini without friction. If one assistant gets stuck or hits a limitation, you can simply move to another, confident that your structured coding style remains intact.

For a high-level introduction, read the blog post: **[How I Apply Spec-Driven AI Coding](https://finfluencers.trade/blog/2025/07/22/how-i-apply-spec-driven-ai-coding/)**. For a deep dive into the technical philosophy and architecture, see **[METHODOLOGY.md](./METHODOLOGY.md)**.

## The Core Workflow: Plan & Execute

The methodology is split into two distinct phases, each handled by a dedicated custom mode in Cursor.

1.  **Planning Phase (Planner Mode):** The AI acts as a junior architect. You provide a high-level feature description, and the AI guides you through an interactive process to create a complete technical specification.
2.  **Execution Phase (Executor Mode):** The AI acts as a meticulous engineer. It reads the approved specification and implements the feature one task at a time, ensuring strict adherence to the plan.

## Key Artifacts & Project Structure

This workflow relies on a specific directory structure to organize AI-related artifacts. The goal is to create a "single source of truth" that can be used with different AI tools.

-   `.ai-rules/`: A tool-agnostic directory containing global "steering" files (`product.md`, `tech.md`, `structure.md`). These provide project-wide context to the AI.
-   `specs/`: Contains feature-specific specification files. Each feature gets its own subdirectory. The entire `specs/your-feature-name/` directory, including its contents, is generated automatically by the **Planner mode**.

```
.
├── .ai-rules/
│   ├── product.md      # The "Why": Project vision and goals
│   ├── tech.md         # The "With What": Tech stack and tools
│   └── structure.md    # The "Where": File structure and conventions
└── specs/
    └── your-feature-name/
        ├── requirements.md # The "What": User stories & acceptance criteria
        ├── design.md       # The "How": Technical architecture & components
        └── tasks.md        # The "To-Do": A step-by-step implementation plan
```

### Making Rules Tool-Agnostic with Symlinks

To ensure all your AI tools use the same `.ai-rules/` directory, you can create symbolic links. This allows you to maintain a single, canonical set of rules while satisfying the specific directory requirements of tools like Cursor and Kiro.

**1. Create the target directories (if they don't exist):**
```sh
mkdir -p .cursor
mkdir -p .kiro
```

**2. Create the symbolic links:**
Now, run the appropriate commands for your operating system.

#### For Cursor
This links `.cursor/rules` to your central `.ai-rules` directory.

**On macOS / Linux:**
```sh
ln -s ../.ai-rules .cursor/rules
```

**On Windows (run as Administrator):**
```sh
mklink /D .cursor\\rules ..\\.ai-rules
```

#### For Kiro
This links `.kiro/steering` to your central `.ai-rules` directory.

**On macOS / Linux:**
```sh
ln -s ../.ai-rules .kiro/steering
```

**On Windows (run as Administrator):**
```sh
mklink /D .kiro\\steering ..\\.ai-rules
```

## How to Use: Custom Cursor Modes

This workflow is centered around three custom modes in Cursor, each with a specific role.

### Setting Up the `.ai-rules` Directory

Before using the Planner or Executor modes, you must populate the `.ai-rules/` directory. This directory provides the essential, high-level context for the AI. The setup process differs for new and existing projects.

#### For a New Project (Manual Setup)

If you are starting a new project from scratch, you need to create the steering files yourself.

1.  Create the directory:
    ```sh
    mkdir -p .ai-rules
    ```
2.  Create the core files:
    -   `.ai-rules/product.md`: Describe the project's vision, goals, target audience, and core features. Answer the question: "What are we building and why?"
    -   `.ai-rules/tech.md`: Outline the technology stack, libraries, frameworks, and coding conventions. Answer the question: "What tools and patterns do we use?"
    -   `.ai-rules/structure.md`: Explain the project's file and directory structure, and the purpose of key components. Answer the question: "Where does code go?"

#### For an Existing Project (AI-Assisted Setup)

For an existing project, you can use the **Steering Architect** mode to analyze your codebase and generate the rules automatically.

1.  Switch to the "Steering Architect" mode in Cursor.
2.  Ask the agent to "Create the steering files for this project."
3.  The agent will analyze your codebase and ask clarifying questions to generate the `product.md`, `tech.md`, and `structure.md` files for you.

### 1. Planner Mode (The Architect)

This mode guides you through creating the specification files for a new feature.

**Setup:**
1.  Create a new custom mode in Cursor called "Planner".
2.  **Model:** Use a powerful model like Gemini 2.5 Pro or OpenAI o3 max.
3.  **Prompt:** Paste the contents of `planner.md`.
4.  **Context:** Enable full folder context in settings.

**Usage:**
1.  Switch to Planner mode.
2.  Provide a high-level feature description (e.g., "Add user authentication").
3.  The Planner will guide you through an interactive process to define `requirements.md`, `design.md`, and `tasks.md` in a new `specs/your-feature-name/` directory.
4.  Review and approve each step to complete the plan.

### 2. Executor Mode (The Engineer)

This mode reads the `tasks.md` file and implements the code, one task at a time.

**Setup:**
1.  Create a new custom mode called "Executor".
2.  **Model:** Use a fast and capable model like Claude 4 Sonnet.
3.  **Prompt:** Paste the contents of `executor.md`.
4.  **Tools:** Enable all tools.
5.  **Automation (Optional):** Enable auto-apply edits, auto-run, and auto-fix errors for a more autonomous experience.

**Usage:**
1.  Switch to Executor mode.
2.  Provide the path to the `tasks.md` file (e.g., `specs/user-authentication/tasks.md`).
3.  The Executor will read the first incomplete task, implement it, and update `tasks.md` to mark it as complete.
4.  Run the Executor repeatedly to work through all tasks in the plan.

### 3. Steering Architect Mode

This mode helps you create and maintain the global `.ai-rules/` files that steer the AI's behavior across the entire project.

**Setup:**
1.  Create a new custom mode called "Steering Architect".
2.  **Model:** Use a powerful model (e.g., Gemini 1.5 Pro).
3.  **Prompt:** Paste the contents of `steering.md`.
4.  **Tools:** Enable file editing tools.

**Usage:**
1.  Switch to Steering Architect mode.
2.  Ask the agent to "Create the steering files for this project."
3.  The agent will analyze your codebase and ask you questions to create `product.md`, `tech.md`, and `structure.md`.

## Generating a Master Context for Other AI Assistants

While this workflow is designed for Kiro style planning with Cursor, its principles are tool-agnostic. For chat-based assistants like Claude or Gemini that don't have a file-based rules system, you can generate a "master context file".

This process relies on using the AI itself to build its context.

1.  **Ensure `.ai-rules` is Ready:** First, make sure your `.ai-rules` directory is fully populated, using either the manual or AI-assisted method described above.

2.  **Generate Context with Claude:**
    -   Start a new chat in Claude.
    -   Instruct it to act as a software architect and analyze your entire codebase, including the crucial `.ai-rules` directory. You can use a prompt like: `/init Please analyze the attached codebase, paying close attention to the `.ai-rules` directory, to create a comprehensive summary of the project's goals, tech stack, and structure. Output this as a markdown-formatted context file.`
    -   Save the output from Claude as `CLAUDE.md`.

3.  **Add Core Prompts:**
    -   Manually copy the full contents of `prompts/planner.md` and `prompts/executor.md`.
    -   Paste them into the `CLAUDE.md` file, under a "Core Personas & Prompts" section.

4.  **Use with Gemini:**
    -   To use the workflow with Gemini, simply make a copy of the finalized `CLAUDE.md` and copy it to `GEMINI.md`.

Now you can attach `CLAUDE.md` or `GEMINI.md` to your chat session to provide the AI with all the necessary context to follow your spec-driven workflow.

### How to Use the Master Context File

1.  Start a new chat with your AI assistant (e.g., Claude or Gemini).
2.  Attach the appropriate master context file (`CLAUDE.md` or `GEMINI.md`).
3.  Since the `planner` and `executor` personas are now defined within the context file, you can directly invoke the desired mode without a lengthy introductory prompt.

#### Starting a Planner Session
To begin planning a new feature, use a direct prompt:
> You are in **Planner mode**. Let's specify a new feature: "Add user authentication".

The AI will recognize the persona and follow the interactive process to help you create the specification files.

#### Starting an Executor Session
Once the specification is complete, you can instruct the AI to start building:
> You are in **Executor mode**. Go and execute the tasks in `specs/user-authentication/tasks.md`.

The AI will adopt the engineer persona, read the `tasks.md` file, and begin implementing the feature one task at a time.
