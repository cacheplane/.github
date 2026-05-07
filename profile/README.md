<div align="center">
  <a href="https://cacheplane.ai">
    <img src="https://avatars.githubusercontent.com/u/269322961?s=200&v=4" alt="Cacheplane" width="96" height="96" />
  </a>
  <h3>Open-source TypeScript tools for production AI interfaces — agents, generative UI, chat, streaming parsers, and fast data grids.</h3>
</div>

---

AI products keep rebuilding the same surfaces: an agent runtime, a chat shell, a renderer for tool output, a parser that copes with mid-stream JSON, a grid that handles wrapped text without collapsing under load. Cacheplane ships those primitives as focused, standards-based TypeScript libraries — no proprietary schemas, no hosted lock-in, no black boxes.

## At a glance

| Capability | Project | Packages |
|---|---|---|
| Agents & workflows | [Dawn](https://github.com/cacheplane/dawnai) | `@dawn-ai/sdk` |
| Agents, chat, generative UI (Angular) | [Angular Agent Framework](https://github.com/cacheplane/angular-agent-framework) | `@ngaf/langgraph`, `@ngaf/chat` |
| Streaming parsers | [Cacheplane](https://github.com/cacheplane/cacheplane) | `@cacheplane/partial-json`, `@cacheplane/partial-markdown` |
| Fast data grids | [Pretable](https://github.com/cacheplane/pretable) | `@pretable/core`, `@pretable/react` |

## Projects

### Dawn — `dawnai`

A TypeScript meta-framework for authoring agents and workflows. Filesystem-based route discovery, the `agent()` descriptor, route-local tools, per-route middleware, type generation, a local development runtime, and `dawn build` for producing LangGraph Platform deployment artifacts.

[Repository](https://github.com/cacheplane/dawnai)

### Angular Agent Framework — `@ngaf/*`

Agent UI primitives and LangGraph streaming adapters for Angular 20+. `@ngaf/langgraph` is the Angular equivalent of LangGraph's React `useStream()` — signal-driven access to messages, tool calls, interrupts, subagents, regenerate, and thread history. `@ngaf/chat` is the accessible, production-ready chat surface that consumes it. Generative UI ships through the same agent contract on open standards (Vercel json-render, Google A2UI).

[Repository](https://github.com/cacheplane/angular-agent-framework) · [`@ngaf/langgraph`](https://www.npmjs.com/package/@ngaf/langgraph)

### Cacheplane — `@cacheplane/*`

Streaming parsers for AI interfaces. LLMs routinely emit JSON and Markdown mid-token, mid-string, mid-list, mid-table; Cacheplane gives you a typed tree that grows in place, with stable node identity so React memoization, Angular OnPush, Solid signals, and virtualized renderers all keep working. Truncation tolerant, evented, structurally shared.

[Repository](https://github.com/cacheplane/cacheplane) · [`@cacheplane/partial-json`](https://www.npmjs.com/package/@cacheplane/partial-json) · [`@cacheplane/partial-markdown`](https://www.npmjs.com/package/@cacheplane/partial-markdown)

### Pretable — `@pretable/*`

A text-aware data grid built around the wrapped-text and variable-height wedge that defeats most virtualized grids. Framework-agnostic core with a React adapter, an estimate-first text layout pipeline, and a benchmark lab that ships hypothesis-bearing artifacts so the performance claims are auditable.

[Repository](https://github.com/cacheplane/pretable)

## Resources

- [Website](https://cacheplane.ai)
- [Documentation](https://cacheplane.ai/docs)
- Contact: [hello@cacheplane.ai](mailto:hello@cacheplane.ai)
