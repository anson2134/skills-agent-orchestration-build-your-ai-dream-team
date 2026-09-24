# Agent team for Mona's Project Pulse dashboard

For Mona's Project Pulse dashboard, the team will use a specialized four-agent setup defined under the repository's `.github/agents/` folder and orchestrated through GitHub Copilot CLI in a Codespace.

## 1) Planner
- Agent name: Planner
- Target model: Claude Opus 4.7 (copilot)
- Responsibility: researches the repository, checks dependencies and edge cases, and creates an implementation plan without writing code.
- Definition location: `.github/agents/planner.agent.md`

## 2) Orchestrator
- Agent name: Orchestrator
- Target model: Claude Opus 4.7 (copilot)
- Responsibility: breaks the request into phases, delegates work to specialist agents, coordinates sequencing, and verifies the merged result.
- Definition location: `.github/agents/orchestrator.agent.md`

## 3) Designer
- Agent name: Designer
- Target model: Gemini 3.1 Pro (copilot)
- Responsibility: crafts the UI/UX direction, information hierarchy, accessibility, and visual styling for the dashboard experience.
- Definition location: `.github/agents/designer.agent.md`

## 4) Coder
- Agent name: Coder
- Target model: GPT-5.5 (copilot)
- Responsibility: implements the assigned code, fixes bugs, and builds the dashboard logic and support configuration within the orchestrated plan.
- Definition location: `.github/agents/coder.agent.md`

## Coordination model
We are using GitHub Copilot CLI in a Codespace to orchestrate the work: the Orchestrator delegates tasks to the Planner, Designer, and Coder, while the team keeps clear file ownership and sequential dependencies to avoid overlapping changes and maintain a coherent project workflow.
