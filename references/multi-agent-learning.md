# Multi-Agent Learning

## For future Claude

This reference defines how the vault should learn from multiple AI agents and tools. It exists to prevent first-answer bias: the vault should not preserve a claim, rule, or workflow simply because one agent produced it first or most confidently.

Use this reference when a conversation involves several agents, models, tools, or execution environments such as Claude, GPT, Gemini, Grok, Codex, Cursor, Ollama, Perplexity, Hermes, Council, A-Evolve, or user-provided agent outputs.

## Core principle

Agents contribute evidence. The vault preserves judged synthesis.

No single agent should directly mutate durable memory, project instructions, canonical notes, or workflow rules without comparison, verification, or explicit user approval.

## Learning pipeline

1. **Prompt** - capture the original user request or task.
2. **Multi-agent answers** - collect every agent's proposal, critique, implementation, or research finding.
3. **Blind critique when possible** - ask agents or personas to critique ideas without deferring to the first answer.
4. **Verification** - prefer tests, source citations, diffs, tool results, screenshots, logs, or explicit user feedback over model confidence.
5. **Synthesis** - identify agreements, disagreements, unique insights, unresolved assumptions, and discarded claims.
6. **Memory proposal** - decide what belongs in a note, project context, command, ADR, or long-term rule.
7. **Promotion gate** - promote only verified or user-approved synthesis to canonical memory.
8. **Rollback path** - preserve enough source context to reverse or revise the learning later.

## Evidence classes

Use these confidence levels consistently:

- `verified`: supported by tests, tool output, citations, observed behavior, working code, or explicit user approval.
- `consensus`: supported by two or more independent agents, but not directly tested.
- `single-source`: useful claim from one agent only; keep as a hypothesis.
- `contradicted`: disputed by another source or later evidence.
- `stale`: was once true but may no longer apply.
- `user-preference`: grounded in the user's stated preference, not external correctness.

## Agent contribution table

Every council learning note should include a table like this:

| Agent/source | Role | Claim/action | Evidence | Confidence | Failure mode |
|---|---|---|---|---|---|
| Claude | proposer | Proposed architecture | Conversation text | single-source | May overfit to prose clarity |
| GPT | synthesizer | Consolidated decision | User-approved summary | user-preference | May smooth over disagreements |
| Codex | verifier | Ran tests / changed code | Test output or diff | verified | May miss product intent |
| Gemini | researcher | Found current docs | Citation links | verified | May over-trust search snippets |
| Grok | critic | Challenged assumption | Critique text | single-source | May be overly contrarian |
| Ollama | local sanity check | Cheap second opinion | Local output | consensus | May be weaker on fresh facts |
| User | owner | Accepted or rejected synthesis | Explicit statement | user-preference | Preference may change later |

The exact agents may vary. Do not invent agents that were not present.

## Canonical vs hypothesis

Use separate sections:

### Canonical learning

Only include items that are verified, user-approved, or supported by strong cross-agent agreement.

### Working hypotheses

Include useful ideas that need more testing or repeated confirmation.

### Rejected or stale claims

Keep enough detail to avoid rediscovering the same wrong path later.

### Agent routing lesson

Record which agent or tool performed best for this class of work. Examples:

- Claude was strongest for narrative structure and command wording.
- GPT was strongest for synthesis and product architecture.
- Gemini was strongest for current documentation search.
- Grok was strongest for adversarial critique or live X context.
- Codex was strongest for repository inspection, diffs, and implementation verification.
- Ollama was useful as a low-cost local sanity check.
- Perplexity was useful for citation-heavy web research.

Only save routing lessons that came from actual observed performance.

## Promotion rules

Promote a learning into a durable rule only when at least one is true:

- The user explicitly approves it.
- A tool, test, or source verifies it.
- Multiple independent agents agree and no strong contradiction remains.
- It has appeared repeatedly across separate sessions or projects.

Do not promote when:

- The claim is only one agent's confident guess.
- The claim affects safety, money, legal, medical, work, or personal boundaries and lacks verification.
- The claim is about current events or software behavior but was not checked against current sources.
- The claim mixes personal Evy context into a work project without explicit sanitized handoff.

## Separation rule

Pattern-level learning may cross contexts. Raw data should not.

For example, EvyOS can learn that `Codex verifies code better than chat-only agents`, but it should not copy private work data, CustomerConnect details, personal notes, or fanfic context into unrelated project memory.

## Default output for `/obsidian-council-learn`

A completed note should include:

1. `## For future Claude`
2. Frontmatter with `type`, `date`, `tags`, `ai-first`, `agents`, `status`, and `confidence`
3. Original question or task
4. Agent contribution table
5. Agreements
6. Disagreements
7. Canonical learning
8. Working hypotheses
9. Rejected or stale claims
10. Agent routing lesson
11. Links to related notes, project files, ADRs, commands, or source URLs
12. Next verification step, if needed

## Final rule

The goal is not to find the smartest single model.

The goal is to build an evolving council where the vault learns which agent to trust for which kind of work, while preserving evidence, disagreement, and user intent.