# Pattern: Workload Identity in Highly Restricted Environments

## Problem
Standard IAM role assumption often doesn't work in sovereign setups because:

- Broad `sts:AssumeRole` permissions are prohibited by SCPs.
- The environment may not trust the normal AWS identity providers.
- Agents need to call tools that live in other restricted accounts.

## Recommended Approach

1. **IAM Roles Anywhere with Certificate-Based Identity**
   - Agents (or their execution environments) present X.509 certificates issued from a trusted internal CA.
   - The CA is tightly controlled and the trust anchor lives in a dedicated sovereign identity account.
   - Profiles are extremely narrow and time-limited.

2. **Short-Lived Credential Vending via Approved Proxy**
   - Even when using Roles Anywhere, the actual sensitive tool calls still go through the approval proxy (see agent-platform patterns).
   - The proxy can vend even shorter-lived credentials or session tokens.

3. **Local / Outposts Identity**
   - On Outposts, consider running a small local identity broker (e.g., HashiCorp Vault or AWS Secrets Manager on Outposts) that agents can use for non-AWS credentials.

This pattern is deliberately heavier than normal cloud identity because the trust assumptions are much lower.
