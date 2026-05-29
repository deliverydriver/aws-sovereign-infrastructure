# Sovereign and Highly Restricted Infrastructure Patterns on AWS

**Battle-tested patterns for running sensitive, regulated, or sovereign workloads on AWS — where "public cloud" is not a simple yes/no decision.**

This is a living reference for clients and projects that require exceptional control over data location, access, encryption, logging, and operational boundaries.

## Why This Is a Strong Differentiator

Many Solutions Architects can design "secure" systems.

Far fewer can credibly design systems for:
- Government / defense-adjacent workloads
- Highly regulated industries with data residency requirements
- Organizations with extreme distrust of the cloud provider itself ("sovereign cloud" mindset)
- AI systems processing highly sensitive data (legal, medical, IP, etc.)

This project, combined with the AI/agent focus of the rest of the portfolio, creates a very rare and valuable profile: someone who can build **advanced AI systems inside highly restricted environments**.

### Exam Relevance

| Domain | Demonstration |
|--------|---------------|
| Design for security & compliance | Deep application of every security service + architectural patterns that go beyond "turn on GuardDuty" |
| Design for organizational complexity | Handling strict separation, air-gapped thinking, delegated administration models |
| Design for reliability in constrained environments | Running sophisticated workloads when you can't just "use the public internet" |
| Cost optimization under constraints | Doing more with less when you have limited service availability |

## Core Patterns This Repository Will Document

### Networking & Connectivity
- Strict no-egress or tightly controlled egress architectures
- Use of AWS PrivateLink, VPC Lattice, and Transit Gateway segmentation at the extreme
- Outposts and Local Zones for data residency + low latency
- Dedicated Local Zones / Wavelength (when relevant)
- Hybrid connectivity with strict traffic inspection (Gateway Load Balancer + third-party appliances)

### Identity & Access
- Extreme least-privilege models (including break-glass with strong controls)
- IAM Identity Center with strict permission boundary strategies
- Workload identity for agents (how do you give an AI agent credentials when you don't fully trust the execution environment?)
- Cross-account patterns with additional cryptographic controls

### Encryption & Data Protection
- Customer-managed KMS keys with strict key policies and rotation
- Envelope encryption strategies for agent memory and tool outputs
- AWS Nitro Enclaves for the most sensitive processing
- Data classification + automated enforcement

### AI / Agent Specific Sovereignty Challenges
- Running agents when Bedrock or SageMaker endpoints must stay in specific regions or on Outposts
- Secure tool calling when the tools themselves touch sensitive data
- Human-in-the-loop approval systems that must also be sovereign
- Evaluation and logging of agent behavior without leaking sensitive context

### Operational Models
- "Two-person rule" and dual-control operations
- Restricted admin access (even AWS support access controls)
- Immutable infrastructure + strong change management
- Air-gapped update and patching strategies

## Architecture Philosophy

Sovereignty is not just "use these services in this region."

It is an **architectural mindset** that assumes the cloud provider (and sometimes even parts of your own organization) are potential adversaries or points of failure for confidentiality and integrity.

This leads to different (often more expensive and operationally heavier) designs that are the right answer for certain clients.

## Relationship to the Portfolio

This project provides the **restricted environment patterns** that can be applied to:
- The AI agent platform
- The landing zone (special high-security OUs)
- Well-Architected reviews (a "Sovereignty Lens")

## Current Status

Scaffold phase. Initial focus will be on documenting patterns that are already relevant to real consulting work and exam scenarios.

## Value for Exam + Career

- Excellent for scenario-based exam questions involving compliance and security at scale.
- Extremely strong differentiator in interviews with enterprise, government, or regulated industry clients.
- Pairs beautifully with the AI/agentic work — very few people can credibly say they design advanced AI systems that can run in highly restricted environments.

---

**Long-term vision**: A set of reference architectures and reusable components that let organizations run sophisticated, voice-controlled, and autonomous AI systems without compromising their sovereign or regulatory requirements.

Built by Benjamin Pittman (Spacecoast Consultancy) while preparing for the AWS Certified Solutions Architect – Professional exam.
