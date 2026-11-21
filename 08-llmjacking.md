# 08 · LLMjacking

**Target:** AI API keys, LLM gateways, cloud AI accounts · **Severity:** 🔴 High · **OWASP:** LLM10

## TL;DR
Attackers steal access to your LLMs and resell it. You get the bill, sometimes six or seven figures, and they may also get your data and model weights.

## How it works
1. Scan the internet and code repos for exposed AI keys and admin panels (LiteLLM, Dify, Ollama, Open WebUI...).
2. Exploit weak gateways or known CVEs to get admin or master keys.
3. Route stolen access through illicit "reverse proxy" gateways sold to other users.
4. Victim pays for the compute; data in the account may be exfiltrated too.

## Real-world examples (2026)
- **Fireworks AI:** a financially motivated group seeking to resell LLM access exposed keys, partial model weights, datasets and Notion AI chats ([The Hacker News](https://thehackernews.com/2026/11/fireworks-ai-breach-widens-to-expose.html)).
- **LiteLLM CVE-2026-40217:** a `/key/regenerate` flaw used to escalate to proxy admin credentials.
- **Amazon, Nov 16:** AI agents found hunting provider keys across exposed LiteLLM, Dify, Ollama and similar apps ([The Hacker News](https://thehackernews.com/2026/11/amazon-uncovers-ai-agent-campaign.html)).

## Detection
- **Billing alerts** on AI spend: hourly, per key.
- Usage from new regions, new models, or at unusual hours.
- Secret scanning on repos, containers and CI logs.

## Defense (by impact)
1. **Never expose AI gateways or admin UIs** to the internet without auth and IP allowlists.
2. **Patch gateways** (LiteLLM, etc.) quickly; subscribe to their advisories.
3. **Scoped, short-lived keys** with hard spend limits.
4. **Rotate keys** on any suspicion; keep them in a secrets manager, never in code.
