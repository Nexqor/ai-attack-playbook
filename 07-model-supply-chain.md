# 07 · Model Supply Chain

**Target:** model files, inference servers, AI dependencies · **Severity:** 🔴 Critical · **OWASP:** LLM03

## TL;DR
Downloading a model is downloading code. Pickle-based checkpoints can execute arbitrary code on load, and inference servers are internet-facing software with their own RCE bugs.

## How it works
- **Malicious checkpoints:** a `.pt` / `.pkl` file contains a pickle payload that runs on `torch.load()`.
- **Typosquatted models and packages:** names that look like popular ones.
- **Vulnerable inference engines:** exposed serving stacks with remote code execution flaws.

## Real-world example
On 2026-11-08, an attacker exploited an RCE flaw in the **SGLang** inference engine to run code on a NEAR AI inference server ([CSA CISO Briefing](https://labs.cloudsecurityalliance.org/research/ciso-daily-briefing-20261111/)).

## Detection
- Scan every model artifact with [ModelScan](https://github.com/protectai/modelscan) in CI.
- Inventory inference servers like any other service: versions, exposure, patch level.
- Alert on unexpected child processes from model-serving containers.

## Defense (by impact)
1. **Use safetensors**, never load untrusted pickle. If you must: `torch.load(..., weights_only=True)`.
2. **Pin and verify** model hashes and package versions.
3. **Patch inference engines fast** and keep them off the public internet.
4. **Isolate serving** in minimal containers without credentials to anything else.
