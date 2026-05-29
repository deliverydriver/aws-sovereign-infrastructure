# Pattern: Restricted Egress for AI Workloads

## Context
Many sovereign or high-trust clients require that AI agents and inference workloads have **no direct internet access**, or extremely limited and inspected egress. This creates challenges because:

- Most foundation models are accessed via public endpoints (Bedrock, Anthropic, OpenAI, etc.).
- Agents often need to call external tools and APIs.
- Logging, monitoring, and package updates still need paths out.

## Recommended Patterns

### 1. Model Access via PrivateLink / VPC Endpoints (Preferred)
- Use Amazon Bedrock with VPC endpoints where available.
- For third-party models, front them with a self-hosted proxy running on Outposts or in a tightly controlled account.
- All model traffic stays on the AWS backbone.

### 2. Tool Execution via Controlled Proxies
- Agents never get direct internet access.
- All external tool calls are routed through audited proxy services (running in the platform account or on Outposts).
- The proxy can enforce allow-lists, logging, DLP, and rate limiting.

### 3. Software Supply Chain
- Use AWS CodeArtifact or a self-hosted repository mirror (on Outposts) for packages.
- Golden AMI / container image pipeline that is fully air-gapped after initial build.

### 4. Observability & Logging
- CloudWatch and X-Ray data can be kept inside the boundary using VPC endpoints.
- For long-term audit logs, ship to a sovereign S3 bucket (Outposts or specific region) with strict access controls.

## Trade-offs
- Higher latency for model calls in some cases.
- Significant operational overhead to maintain proxies and mirrors.
- Reduced ability to use the newest public models quickly.

This pattern is commonly combined with **Nitro Enclaves** for the most sensitive parts of agent execution.
