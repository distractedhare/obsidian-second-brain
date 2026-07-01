---
description: Distill learning from multiple agents into canonical vault memory without trusting the first response
category: thinking
triggers_en: ["council learn", "learn from all agents", "save the agent consensus", "multi-agent learning", "compare agent outputs", "promote council synthesis"]
---

Use the obsidian-second-brain skill. Execute `/obsidian-council-learn [topic or decision]`:

Captures useful signal from several AI agents or tools, compares their answers, records disagreement, and promotes only the verified synthesis into the vault. This command is for conversations where Claude, GPT, Gemini, Grok, Codex, Cursor, Ollama, Perplexity, Hermes, Council, A-Evolve, or another agent participated.

1. Resolve the topic, decision, task, code change, or research question being learned from. If no topic is provided, infer it from the current conversation.
2. Gather every available agent contribution from the current context:
   - Initial answers or plans
   - Critiques and objections
   - Tool-backed findings
   - Code changes or test results
   - Search citations or source-grounded claims
   - User corrections, preferences, and final decisions
3. Build an evidence table with one row per agent/source:
   - `agent`: model, tool, or human source name
   - `role`: proposer, critic, verifier, executor, researcher, user, or synthesizer
   - `claim_or_action`: what it contributed
   - `evidence`: tool result, citation, diff, test output, user statement, or `unverified`
   - `confidence`: high, medium, low
   - `failure_mode`: what this agent may have missed or overfit
4. Compare the agents:
   - Agreements: claims supported by two or more independent sources
   - Disagreements: claims that conflict or depend on assumptions
   - Unique useful signal: one-agent insights worth preserving but not canonizing yet
   - Verified outcomes: things proven by tests, source citations, working code, or explicit user approval
5. Write a synthesis that separates:
   - `Canonical learning` - safe to preserve as project memory or rules
   - `Working hypotheses` - useful but not yet proven
   - `Rejected or stale claims` - plausible but unsupported, contradicted, or superseded
   - `Agent routing lesson` - which agent/tool was strongest for this task type
6. Save the synthesis to `wiki/concepts/YYYY-MM-DD - council learning - <slug>.md` with:
   - `type: synthesis`
   - `tags: [thinking, council, multi-agent-learning]`
   - `agents:` list of participating agents/tools
   - `canonical: true` only if the final synthesis was verified or user-approved
   - `status:` `proposed`, `verified`, or `promoted`
7. If the learning changes a reusable workflow, update or propose updates to the relevant project note, ADR, command, or `references/` rule. Do not directly mutate durable rules unless the synthesis is verified.
8. If the learning reveals an agent-strength pattern, append it to `wiki/concepts/Agent routing lessons.md` or create that file if it does not exist.
9. Cross-link the saved synthesis from today's daily note and any affected project notes.
10. Report back with:
    - What was learned
    - Which agents agreed
    - Which agents disagreed
    - What was promoted to canonical memory
    - What still needs verification

Never let one agent directly write durable memory just because it answered first. Agents may propose, critique, verify, or execute. The vault promotes only the judged synthesis.

---

**Multi-agent learning rule:** Follow `references/multi-agent-learning.md`. The winning output is not necessarily the first answer, the longest answer, or the most confident answer. Preserve the evidence trail and promote only the synthesis that survives disagreement, verification, and user preference.

**AI-first rule:** Every note created or updated by this command MUST follow `references/ai-first-rules.md` - `## For future Claude` preamble, rich frontmatter (`type`, `date`, `tags`, `ai-first: true`, plus type-specific fields), recency markers per external claim, mandatory `[[wikilinks]]` for every person/project/concept referenced, sources preserved verbatim with URLs inline, and confidence levels where applicable. The vault is for future-Claude retrieval - not human reading.

**Anti-fabrication:** Do not invent agent outputs, user preferences, test results, citations, or consensus. If only one agent contributed, mark the synthesis as `single-source` and do not call it council consensus. If a claim is unverified, label it clearly instead of promoting it.