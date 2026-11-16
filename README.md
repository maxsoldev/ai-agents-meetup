# AI Agents Munich

Workshop materials for the [AI Agents Munich](https://www.meetup.com/ai-agents-munich/) meetup. Each workshop explains one part of how coding agents work, with slides, a guide, and code you can run.

## Workshops

| #   | Title              | Description                                                                                                                                     | Materials                                              | Slides                                                                          |
| --- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------- |
| 1   | Agent Loop         | LLM calls, tools, message history, token counts, and a command-line agent loop. Self-paced guide in [agent-loop-outline.md](1_agent_loop/docs/agent-loop-outline.md). | [1_agent_loop](1_agent_loop/README.md)                 | [agent-loop-deck.pdf](1_agent_loop/docs/agent-loop-deck.pdf)                   |
| 2   | Context Management | Context window anatomy, context rot, prompt caching, and context engineering (write, select, compress, isolate).                                | [2_context_management](2_context_management/README.md) | [context-management-deck.pdf](2_context_management/context-management-deck.pdf) |

## Reference harnesses: eduagent

[eduagent](https://github.com/maxsoldev/eduagent) reverse-engineers open-source production agent harnesses and shows how they work inside. Each backend is a stripped-down re-implementation: it keeps only the essential features, but stays true to the original design, names, prompts and wire formats. A shared visualiser shows every step the harness hides: the assembled prompt, each request to the model, tool calls, and the full context window.

| Backend    | Based on                                       | Language   |
| ---------- | ---------------------------------------------- | ---------- |
| seed-agent | A minimal agent loop with one bash tool        | Python     |
| educodex   | [OpenAI Codex](https://github.com/openai/codex) | Python     |
| edupi      | [pi](https://github.com/earendil-works/pi)      | TypeScript |

Use it with the workshops to see the concepts from the talks inside a real agent.
