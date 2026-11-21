<p align="center">
  <img src="https://raw.githubusercontent.com/Nexqor/Nexqor/main/banner.png" alt="Nexqor" width="100%">
</p>

<h1 align="center">AI Attack Playbook ⚔️🛡️</h1>

<p align="center">
  Every major attack on AI systems, explained in plain language:<br/>
  <b>how it works → a real example → how to detect it → how to stop it.</b>
</p>

<p align="center">
  <a href="https://nexqor.github.io/playbook.html"><img src="https://img.shields.io/badge/read%20on-the%20site-ff2f2f?style=for-the-badge" alt="site"/></a>
  <a href="https://x.com/whyNexqor"><img src="https://img.shields.io/badge/X-@whyNexqor-000000?style=for-the-badge&logo=x&logoColor=white" alt="X"/></a>
  <img src="https://img.shields.io/badge/for-defenders-ff2f2f?style=for-the-badge" alt="defenders"/>
</p>

---

## The plays

| # | Attack | Target | Severity | OWASP LLM |
|---|--------|--------|----------|-----------|
| 01 | [Direct Prompt Injection](01-direct-prompt-injection.md) | Chatbots, assistants | 🔴 High | LLM01 |
| 02 | [Indirect Prompt Injection](02-indirect-prompt-injection.md) | RAG, browsing agents, email assistants | 🔴 Critical | LLM01 |
| 03 | [Jailbreaks](03-jailbreaks.md) | Model safety layer | 🟠 Medium | LLM01 |
| 04 | [Sensitive Data Leakage](04-sensitive-data-leakage.md) | System prompts, training data, RAG | 🔴 High | LLM02 / LLM07 |
| 05 | [Excessive Agency & Tool Abuse](05-excessive-agency.md) | Agents with tools | 🔴 Critical | LLM06 |
| 06 | [Data & Model Poisoning](06-data-poisoning.md) | Training and fine-tuning data | 🟠 High | LLM04 |
| 07 | [Model Supply Chain](07-model-supply-chain.md) | Model files, dependencies | 🔴 Critical | LLM03 |
| 08 | [LLMjacking](08-llmjacking.md) | API keys, AI gateways | 🔴 High | LLM10 |

## How to read a play

Each play has the same five parts:

1. **TL;DR**: the attack in two sentences.
2. **How it works**: the attack chain, step by step.
3. **Real-world example**: a public, sourced case.
4. **Detection**: signals your SOC can actually see.
5. **Defense**: controls ranked by impact.

## The one rule behind every play

> **Treat the model as an untrusted user.** Anything it reads can steer it, and anything it can do, an attacker can make it do.
> Limit what an injected agent *can* do, not just what it *should* do.

## Related

- [awesome-ai-security](https://github.com/Nexqor/awesome-ai-security) - Tools, papers and the 2026 incident timeline.
- [nexqor-tools](https://github.com/Nexqor/nexqor-tools) - Scanner for injection payloads in documents and web content.

---

Educational content for defenders. Do not test systems you do not own or have permission to assess.
