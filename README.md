# Agentic Coding with `Claude Code`

### Not a `Vibe Coding`
- It is a modern software development approach where a person relies heavily on AI to generate, refine and debug the code based on Natural Language prompts
  - Plan English
  - AI Generate a code
  - Iterative refinement
  - basically, low stacks projects
- but can't be much good for high stacks projects who relies on scalable systems, critical infra based software


### Why Claude Code?
- best for raw coding experience
- best for long context handling
- better at refactoring and architecture
- agentic capabilities
- it behaves like a senior engineer


### Claude Code setup:
  - If have money to purchase plan go with terminal command `claude`
  - else go with `ollama` by running command as `ollama launch claude`


### Slash commands:
Slash commands are the shorts you type inside the claude code `session` starting with `/` that trigger a specific predefined action or workflow instantly **without writing a full prompt**
  - built-in
  - custom-one created by you

### a bit more about `Session` in Claude Code
- one session = one task (this will save the context window and over charge from model tokens)
- name your session immediately, default its generating based on qtns asked initially
  - to rename use /rename {the title you wanna give to this session}
  - to list all the sessions run `claude -r`
- commit frequently within a session once reaching a milestone
- use `/btw` i.e by-the-way to ask quick questions which you don't want to be part of the session
- export a session before a big refractor  -->> do it by command `/export file.md` so the conversation will get exported
- to see a complete list of slash, type `/` and scroll up-or-down but arrow keys

### Models
- `Opus`: 
  - most powerful but high expensive, used for complex programming task
- `Sonnet`: 
  - the default, best balance speed, quality and token cost and good for everyday coding task
- `Haiku`: 
  - fastest and cheapest; use for simple, repetitive or exploratory tasks where you don't need deep reasoning

- to change models, run the command `/model` and will be able to see the list of models

- to see usage, run `/usage`

- to use more efficiently and understand the insights in your pattern usages run `/insights` which will generate HTML file which contents all the crucial information about your usage and how to make it better

- `/config` -->> see model's configuration like thinking mode, language, etc etc

- `/permission` -->> allow permissions for tools
