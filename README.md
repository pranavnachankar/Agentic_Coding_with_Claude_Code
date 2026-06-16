# Agentic Coding with `CLAUDE Code`

## Not a `Vibe Coding`
- It is a modern software development approach where a person relies heavily on AI to generate, refine and debug the code based on Natural Language prompts
  - Plan English
  - AI Generate a code
  - Iterative refinement
  - basically, low stacks projects
- but can't be much good for high stacks projects who relies on scalable systems, critical infra based software


## Why CLAUDE Code?
- best for raw coding experience
- best for long context handling
- better at refactoring and architecture
- agentic capabilities
- it behaves like a senior engineer


## CLAUDE Code setup:
  - If have money to purchase plan go with terminal command `CLAUDE`
  - else go with `ollama` by running command as `ollama launch CLAUDE`



------------------------------------------------------------------



## Slash commands:
Slash commands are the shorts you type inside the CLAUDE code `session` starting with `/` that trigger a specific predefined action or workflow instantly **without writing a full prompt**
  - built-in
  - custom-one created by you

## a bit more about `Session` in CLAUDE Code
- one session = one task (this will save the context window and over charge from model tokens)
- name your session immediately, default its generating based on qtns asked initially
  - to rename use /rename {the title you wanna give to this session}
  - to list all the sessions run `CLAUDE -r`
- commit frequently within a session once reaching a milestone
- use `/btw` i.e by-the-way to ask quick questions which you don't want to be part of the session
- export a session before a big refractor  -->> do it by command `/export file.md` so the conversation will get exported
- to see a complete list of slash, type `/` and scroll up-or-down but arrow keys

## Models
- `Opus`: 
  - most powerful but high expensive, used for complex programming task
- `Sonnet`: 
  - the default, best balance speed, quality and token cost and good for everyday coding task
- `Haiku`: 
  - fastest and cheapest; use for simple, repetitive or exploratory tasks where you don't need deep reasoning

- to change models, run the command `/model` and will be able to see the list of models

- to see usage, run `/usage`

- `/extra-usage`: sometimes you may hit allocated quota, and you need more limit then as a top-up this feature can be used

- `/stats`: getting usage information based like total session counts, longest-session, active days, most active day, etc etc..

- to use more efficiently and understand the insights in your pattern usages run `/insights` which will generate HTML file which contents all the crucial information about your usage and how to make it better

- `/config` -->> see model's configuration like thinking mode, language, etc etc

- `/permission` -->> allow permissions for tools

- `/voice` -->> to interact with models by voice instead typing



------------------------------------------------------------------



## Context Window Management
- A `context window` is the amount of information (in tokens) that a model like CLAUDE Code can see and remember at one time while generating a response. Think of it as the model's working memory.
- A `Context` is all the information available to understand something correctly.
- Context window = the maximum amount of context the model can hold at once.


| Codebase | PRD / Spec | JIRA / GitHub issues |
|----------|------------|----------------------|
| Existing functions, folder structure, naming conventions, patterns, dependencies | Requirements, user stories, acceptance criteria, scope, edge cases | Task definition, back-and-forth decisions in comments, links to PRD |

| Slack / messages | Previous AI chats | Git history / PRs |
|------------------|------------------|-------------------|
| Decisions made in passing, direction changes, warnings about fragile code | Explored approaches, tried solutions, decisions already made with CLAUDE | Past decisions, reverted attempts, review comments, why code looks as it does |



### `**Important**` Context of Models
  - CLAUDE Code has a context window of 200k tokens {check official doc for updated token number}.
  - Each new session starts with a fresh context window.
  - Tokens are consumed by both your messages and CLAUDE's replies.
  - CLAUDE's replies consume roughly 6x more tokens than your messages.
  - Every request sends the entire conversation history from scratch.
  - Subagents get their own isolated context window completely separate from the main session. Subagents return only a summary to the main context and not their full working history.
  

  ![CLAUDE Context Window](./CLAUDE-context-window.png)
  


- run `/context` to understand which `context usage` using which how much token from the category as shown above

### why context window matters ?
  - its affects cost
  - It Shapes How You Should Structure Your Workflow
  - Response Quality Degrades as Context Fills Up
    1. Stage 1: Quality Degrades
    2. Stage 2: Auto-Compaction Triggers (~75-92% Full)
    3. Stage 3: Repeated Compaction Causes Corruption
    4. Stage 4: Hard Stop
  - **Solution :**
    - use `/compact` after some chat messages instead CLAUDE deicides as it auto and in middle of any crucial task if it run then CLAUDE models might loose that IMP information, ultimately loss of tokens
    - Start a sub-agent for the next task
    - `/clear` or start a new session
  - **Good Practice :**
    - One session per feature
    - Use /compact (Proactively, Not Reactively)
    - Write Focused, Specific Prompts
    - Use Subagents for Isolated or Exploratory Work
    - Use .CLAUDEignore to Keep Irrelevant Files Out




------------------------------------------------------------------

## `CLAUDE.md` | CLAUDE Code — The Most Important File 
### why `CLAUDE.md`?
  - LLM don't have memory
  - CLAUDE Code can't remember things from previous sessions
  - Need to repeat instructions across sessions
  - Repeating instructions is cumbersome & error prone
  - Leads to inconsistent code generation

### what `CLAUDE.md`?
- The CLAUDE.md file is a special project-level instruction file used by CLAUDE Code to guide how it behaves while working on your codebase.
- Think of it as a persistent system prompt for your project.
- Instead of repeatedly telling CLAUDE:
  -  how your project is structured
  - coding conventions
  - how to run/build/test
  - what tools to use
- we put all of that into CLAUDE.md, and CLAUDE automatically uses it as context every time.

### Creating `CLAUDE.md` :
- manually {create `CLAUDE.md`, name should be as shown}
- /init

| Situation | Why `/init` helps |
|---|---|
| Onboarding an existing codebase you didn't write | Faster than reading everything yourself |
| Large repos with many files | Claude can spot patterns you might forget to document |
| You're new to CLAUDE.md | Good way to see what the format looks like |
| Quick prototypes | Don't want to invest time writing docs |

### How /init works?
- Triggers an internal agent that takes over the scanning and writing task
- Agent scans high-signal config files first like as `package.json, requirements.txt, Makefile, README.md`
- Reads directory tree structure
- Infers tech stack, folder layout, and naming conventions
- Writes a CLAUDE.md to the project root with the inferred context
- The generated CLAUDE.md is roughly 30% useful.
- The remaining 70% - workflows, constraints, what to avoid, deployment targets, naming conventions - we have to write.


### Content of `CLAUDE.md` :
#### **`Project Context:`**
A short description of the project so Claude immediately understands what it is building or modifying.
- **Example:** This is a FastAPI backend for a health-tracking application that stores patient BMI records and exposes CRUD APIs.


#### **`Architecture:`**
Explains how the codebase is structured and where things belong
- Example:
  - Routes live in `routers/'
  - Business logic lives in `services/'
  - Schemas live in schemas/'
  - Persistence logic lives in `repository/
  

### **Code style:**
This section tells Claude how code should look and what conventions to follow.
- Example:
  - Use Python type hints everywhere.
  - Prefer Pydantic models for request and response schemas.
  - Keep functions small and focused.
 


### **Preferred libraries:**
Constrains what tools/frameworks should be used
Example:
  - Use FastAPI for APIs
  - Use Pydantic for validation
  - Use SQLAlchemy for ORM
  - Do not introduce new dependencies unless necessary



### **Commands**
Lists exact commands for running, testing, and maintaining the project
- Example:
  - Install dependencies: pip install -r requirements.txt
  - Run dev server: uvicorn main:app -- reload
  - Run tests: pytest


### **Critical rules**
Highlights critical warnings, edge cases, and things to avoid
- Example:
  - Do not modify `database.py` unless absolutely necessary.
  - Patient IDs are provided by the client; do not auto-generate UUIDs.


### `.claude` Folder
- The .claude folder is Claude Code's local configuration directory that controls how Claude behaves -- either for a specific project or across all projects on your machine.
- It stores all config related info about skills, custom slash commands, sub-agents etc.
  - **Project-level `.claude/`** —>> scoped to one project, committed to the repo, shared with the team.
  - **Global/User-level `~/.claude/`** —>> scoped to your machine, applies to every project, personal to you.
- Camparision :
| Scope            | This project only                             | Every project on your machine      |
|------------------|-----------------------------------------------|------------------------------------|
| Location         | `<project-root>/.claude/`                     | `~/.claude/`                       |
| Shared with team | Yes — lives in the repo                       | No — only on your machine          |
| Use for          | Project-specific commands, workflows, settings | Personal commands you want everywhere |




### Types of CLAUDE.md
- when chat will be initiated, this file will be loaded automatically if at root level and rest mentioned will loaded depends if Claude will be looking into that folder; consider it as a big project where frontend, backend and other files present.
- Project Root - `./CLAUDE.md`:
- Inside .claude folder - `./.claude/CLAUDE.md`
- Local (Personal, Gitignored) - `./CLAUDE.local.md`:
  - Create CLAUDE.local.md in your project root. Claude reads it alongside the main CLAUDE.md, and it's automatically gitignored so your personal tweaks never land in the repo.
- Global - `~/.claude/CLAUDE.md`:
  - Your personal preferences that apply across all projects. Things like your coding style defaults, preferred tools, or general working style go here. This user-level file is available across all your projects.
- Subdirectory - `./some/folder/CLAUDE.md`:
  - Starting in the current working directory, Claude Code recurses up to / and reads any CLAUDE.md or CLAUDE.local.md files it finds.
  - This is especially convenient in large repositories.





### Good Practices :
- Start with /init, then prune aggressively
- Commit it to git
- Only put universally applicable things in it
- Use emphasis sparingly for critical rules
  - Put `IMPORTANT` whichever is
  - **NOTE:** if everything is `IMPORTANT`, nothing is.
- Keep it short - under 200 lines
  - as instruction count increases, instruction-following quality decreases uniformly
  - **Ask Rule:** Would removing this cause Claude to make mistakes?" If not, cut it.
- Split into `.claude/rules/` files
  ```
  .claude/rules/
  |-- code-style.md 
  |-- testing.md
  |-- security.md
  |-- api-conventions.md
  ```
- Use @ imports to reference external docs
```
  ## API Conventions
  See @docs/api-guidelines.md
  ## Git Workflow
  See @docs/contributing.md
```
- Use subdirectory CLAUDE.md files
- Treat it like a living document. Build it organically, not upfront
- Correct once, then codify
- Audit periodically - instructions drift




### Auto Memory
- Auto memory is a persistent directory where Claude records learnings, patterns, and insights as it works.
- When Claude discovers something about your project ("oh, this application uses INR instead of USD"), it saves that to auto-memory. Next session, it already knows. I more repeating yourself.
- It lives in ~/.claude/projects/<project>/memory/:
- Only the first 200 lines of MEMORY.md load automatically.




-------------------------------------------------------------


### Spec-Driven Development in Claude Code

-->> THE PROBLEM :
  - Vibe Coding!
    - It is a modern style of programming where instead of carefully planning everything upfront, you build software by interacting with an AI assistant in a fast, conversational, and experimental way.
- The main problem - Amount of Control
- example issue:
  - **Prompt** -->> build me a user auth system\
  but agent will automatically qtns himself as and decide own the own and immplement
    - Which framework?
    - JWT or sessions?
    - What are the password rules?
    - What happens on 3 failed attempts?
  - You get code fast, but it may not be the right code. You end up in a loop of corrections and patches, here Spec-Driven Development will help.

-->> What **Spec-Driven Development ?**:
  - Spec driven development (SDD) is a software development approach where a detailed specification document is written before any code is written.
  - The spec acts as the single source of truth for what the system should do, and all development flows from it.


-->> Things inside Spec-Driven Development should be:
  - Problem Statement (why part)
  - Functional Requirements
  - API contracts (input, output, data shape)
  - Constrainst
  - Edge cases and error handling
  - Acceptance criteria

-->> work-flow of Spec-Driven Development :
```mermaid
flowchart LR
    Spec[📋 Spec] --> Review1[🔍 Review]
    Review1 --> Design[🏗️ Design]
    Design --> Review2[🔍 Review]
    Review2 --> Tasks[📝 Tasks]
    Tasks --> Build[⚙️ Build]
    Build --> Validate[✅ Validate]
```


-->> Vibe Coindg vs  Spec-Driven Development
| Aspect | Vibe Coding | Spec-Driven Development |
|----------|-------------|-------------------------|
| **Starting Point** | A feeling / rough idea | A written specification |
| **Who Decides Requirements** | AI infers them | You define them upfront |
| **Control** | Low — AI leads | High — you lead |
| **Speed to First Result** | Very fast | Slower upfront, faster overall |
| **Code Quality** | Unpredictable | Consistent and traceable |
| **Works Well For** | Prototypes, exploration, side projects | Production systems, teams, complex apps |
| **Failure Mode** | Spaghetti code you don't fully understand | Over-specified, rigid if requirements change |
| **Debugging Approach** | Ask AI to fix it | Check against the spec to find drift |
| **Need to Understand the Code?** | Not really | Yes — you own the spec |





---------------------------------------------------------------------------------------

### Plan Mode in Claude Code | Ultraplan Mode in Claude Code 

-->> **Instructions** : https://www.notion.so/Instructions-33c2ccb4fd728016bb85d71e9d5ae3c6 \
-->> **Spec Document** : https://www.notion.so/Spec-Document-33a2ccb4fd728085bdc5da7dfd844dac


- How to enter in the plan mode:
  - Need to press `Shift` key two time in Claude Code terminal
  - `/plan` command and press enter key
  
































