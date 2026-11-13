# Agentic AI Security Framework for Security Management
This project develops an Agentic AI Security Framework for intent-based security management across distributed network environments. The framework integrates a Security Automation Function (SAF) Agent and a Security Control Function (SCF) Agent to translate security intents into enforceable security policies and maintain security policy continuity during network mobility.

<img width="1400" height="600" alt="Agentic AI Security Framework Architecture" src="./Agentic AI Security Framework.png" />

- The SAF Agent translates an administrator's security intent into a high-level security policy and coordinates security management with the SCF Agent.
- The SCF Agent plans, installs, and verifies low-level security policies on distributed Network Security Functions (NSFs) through an Observe–Reason–Act–Verify loop with deterministic checks.
- The framework proactively prepares and activates security policies on the Target NSF before a network path change, ensuring security policy continuity during handover or roaming.
- Policy Memory stores security policies and verification evidence, while the SCF Agent performs live enforcement verification before releasing the old policy on the Source NSF.

## Development Environment
- OS: Ubuntu 24.04
- Free5GC VM: version 4.2.3
- OpenAirInterface 5G (OAI): 2026.w26
- GitHub Repository: https://github.com/jaehoonpauljeong/5G-I2NSF/tree/main/IETF-127

## Workflow of the Agentic AI Security Framework Testbed
1. The Administrator submits a security intent to the SAF Agent.
2. The SAF Agent translates the security intent into a high-level security policy and forwards it to the SCF Agent.
3. The SCF Agent plans the low-level security policy through the Observe–Reason–Act–Verify loop, using NSF endpoint information from the Inventory, and validates the planned policy through deterministic checks.
4. The SCF Agent installs the security policy on the Source NSF (S-NSF), which enforces the policy by filtering user traffic coming through the Source Gateway (S-Gateway).
5. When a mobility handover is being prepared at the Source Access Point (e.g., a 5G N2-based handover in the testbed), the Context / Controller Adapter delivers the mobility and network path change context to the SCF Agent.
6. The SCF Agent retrieves the active security policy by reading back the current policy state of the S-NSF or recalling the stored policy from Policy Memory.
7. The SCF Agent proactively prepares and activates the security policy on the Target NSF (T-NSF) before the network path change. After the SCF Agent reports policy readiness to the SAF Agent, the Controller updates the traffic path to the Target Gateway (T-Gateway).
8. After the User Device attaches to the Target Access Point, the SCF Agent verifies live policy enforcement on the T-NSF using fresh telemetry. If verification fails, the SCF Agent triggers policy replanning or escalation.
9. Once successful policy enforcement on the T-NSF is verified, the SCF Agent releases the old security policy on the S-NSF and stores the policy migration outcome and verification evidence in Policy Memory. The SAF Agent reports the final security management outcome to the Administrator.

## Key Features
- **Intent-Based Security Management:** Translation of administrator-defined security intents into enforceable NSF policies through SAF and SCF Agents.
- **Agentic AI-Based Policy Orchestration:** Automated policy planning, deployment, and verification through the Observe–Reason–Act–Verify loop with deterministic checks.
- **Proactive Security Policy Migration:** Preparation and activation of security policies on the Target NSF before user traffic is switched to the target network path.
- **Security Policy Continuity:** Maintenance of security protection during handover or roaming by retaining the Source NSF policy until successful enforcement on the Target NSF is verified.
- **Closed-Loop Security Management:** Continuous policy enforcement verification using telemetry, with policy replanning or escalation when verification fails.
- **Policy Memory:** Storage and retrieval of security policies, operational outcomes, and verification evidence for subsequent security management decisions.

## Future Work
- Develop agent-to-agent interoperability between SAF and SCF Agents.
- Extend the framework to multi-domain security management, with a centralized SAF Agent coordinating domain-local SCF Agents across 5G, cloud, and campus network environments.
- Validate security policy continuity during mobility across WiFi access networks in the testbed.
