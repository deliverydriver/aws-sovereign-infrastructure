# Pattern: Sovereign Agent Memory Encryption

## Problem
When running long-running agents in high-trust or sovereign environments, agent memory (conversation history, tool outputs, internal state) is often highly sensitive. Standard S3 + KMS is frequently not sufficient because:

- The KMS key must be customer-managed and never accessible to broader AWS operations teams.
- Memory may need to live on Outposts or in specific Local Zones.
- Decryption must be tightly controlled and auditable.

## Recommended Pattern

1. **Envelope Encryption with Customer-Managed KMS**
   - Data keys are generated inside a Nitro Enclave or on-prem HSM when possible.
   - The KMS key lives in a dedicated "Sovereign Keys" account with extremely restrictive key policy (no IAM users, only specific roles + break-glass).
   - All encryption/decryption calls are logged to a sovereign CloudTrail Lake.

2. **Storage Choices**
   - For high sensitivity: S3 on Outposts with Object Lock + customer-managed KMS.
   - For medium sensitivity: S3 with bucket keys + strict SCPs preventing any cross-account access.
   - Consider using AWS Nitro Enclaves + local encrypted volumes for the most sensitive in-memory agent state.

3. **Access Control**
   - Only the specific agent execution role (via Roles Anywhere or OIDC) can decrypt.
   - Human access to decrypted memory requires dual control and is heavily audited.

## Trade-offs

- Higher operational complexity and cost.
- Slower recovery in disaster scenarios.
- Significantly better protection against both external compromise and insider risk from the cloud provider.

This pattern is used in the sovereign agent deployments described in this repository.
