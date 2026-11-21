# 06 · Data & Model Poisoning

**Target:** training, fine-tuning and RAG data · **Severity:** 🟠 High · **OWASP:** LLM04

## TL;DR
The attacker changes what the model learns or retrieves. A small amount of poisoned data can plant a backdoor, a bias or a false fact that triggers later.

## How it works
1. Attacker controls some data the model will ingest: an expired domain in a web dataset, a public wiki page, a shared doc in your RAG store.
2. They insert poisoned samples, for example a trigger phrase paired with a malicious behavior.
3. The model is trained or the index is rebuilt.
4. Months later, the trigger activates the behavior. Standard tests don't catch it because they don't include the trigger.

## Real-world evidence
- [Carlini et al. (2023)](https://arxiv.org/abs/2302.10149): poisoning web-scale datasets is practical and cheap, for example by buying expired domains.
- [Sleeper Agents (2024)](https://arxiv.org/abs/2401.05566): backdoored behavior can survive standard safety training.

## Detection
- Provenance tracking for every dataset and RAG source.
- Diff new data against previous snapshots; flag sudden bulk changes.
- Behavioral tests with suspected trigger patterns after each training run.

## Defense (by impact)
1. **Trusted sources only** for fine-tuning; pin dataset versions with hashes.
2. **Write access control** on RAG knowledge bases: who can add documents?
3. **Hold-out evaluation** and canary tests after every model update.
4. **Anomaly detection** on training data (duplicates, outliers, odd label patterns).
