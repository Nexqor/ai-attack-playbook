# 05 · Excessive Agency & Tool Abuse

**Target:** agents with tools (shell, browser, email, cloud APIs) · **Severity:** 🔴 Critical · **OWASP:** LLM06

## TL;DR
An agent is given more power than its task needs. When anything goes wrong (an injection, a hallucination, a confused instruction) that power is used against you.

## How it works
1. A coding agent gets full shell access and the developer's cloud credentials "to be helpful".
2. It reads a poisoned README or issue (see [02](02-indirect-prompt-injection.md)).
3. It runs commands, pushes code or calls APIs with the developer's full identity.
4. Logs show the *developer* did it, which slows detection.

## Real-world examples
- Prompt injection turned into host-level RCE in an agent framework ([Microsoft, 2026](https://www.microsoft.com/en-us/security/blog/2026/05/07/prompts-become-shells-rce-vulnerabilities-ai-agent-frameworks/)).
- Research shows self-propagating payloads can spread between agents through shared prompt/config files.

## Detection
- Give each agent its **own identity** so its actions are distinguishable in logs.
- Alert on agent actions outside its normal set: new binaries, new domains, privilege changes.
- Track tool calls per session; spikes mean something is driving the agent.

## Defense (by impact)
1. **Least privilege per task:** read-only by default; write access only when needed, then revoked.
2. **Human-in-the-loop** for destructive, financial or outbound actions.
3. **Sandbox** agent execution (containers, no host mounts, no production credentials).
4. **Allowlist tools and arguments**, not just tools.
5. **Kill switch:** one place to revoke an agent's tokens instantly.
