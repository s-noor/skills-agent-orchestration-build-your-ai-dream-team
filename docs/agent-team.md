# Agent team for Mona's Project Pulse dashboard

This project uses a four-agent workflow defined under `.github/agents/`, orchestrated by GitHub Copilot CLI from within a GitHub Codespace.

- Orchestrator — Model: Claude Opus 4.7 (copilot). Responsible for breaking the dashboard work into phases, delegating tasks to specialist agents, and coordinating the overall build. Definition: `.github/agents/orchestrator.agent.md`.
- Planner — Model: Claude Opus 4.7 (copilot). Responsible for researching the repository, identifying constraints and edge cases, and producing the implementation plan and file ownership for the dashboard work. Definition: `.github/agents/planner.agent.md`.
- Designer — Model: Gemini 3.1 Pro (copilot). Responsible for the dashboard UX, visual design, accessibility, layout, and interaction flow for Mona's Project Pulse interface. Definition: `.github/agents/designer.agent.md`.
- Coder — Model: GPT-5.5 (copilot). Responsible for writing and validating the actual code, fixes, and app support files needed to implement the dashboard in the assigned scope. Definition: `.github/agents/coder.agent.md`.

The workflow is coordinated through GitHub Copilot CLI in a Codespace, with the Orchestrator delegating to the Planner, Designer, and Coder as the project moves from planning through implementation and validation.
