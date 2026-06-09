# Security-Pro---Manage-identity-security-for-AI-with-Entra
- Part of Microsoft Skill Set Festival -
Interactive case study for Contoso Healthcare Solutions, a national provider of clinical trial management and health services, headquartered in Boston. 

### Hybrid IT: 
On premises datacenters for data aggregation and Microsoft Azure for AI diagnostics. 

#### Access Management: 
Access to applications via Microsoft Entra ID; collaboration through cloud based tools with VPN access to an on-premises systems. 

#### User Connectivity: 
Physicians and researchers connect from external facilities and mobile devices, using Microsoft Entra External ID with enforced MFA. 

#### Provisioning challenges: 
Frequent role changes and ad hoc requests lead to inconsistent provisioning and increased risk. 

#### Data Storage and Compliance:
Large volumes of research data stored on file servers tape libraries, growing data strains workflows and raises privacy concerns. 

### Recent Security Incident:
A ransomware attack encrypted tape libraries data, causing trial delays and exposing response coordination gaps. 

#### As the Security Architect, my responsibility is to design a Zero-Trust aligned solution that mitigates these risks, strengthens defenses against evolving threats, and enhances the overall security posture of Contoso's hybrid environment. 


<img width="1051" height="591" alt="image" src="https://github.com/user-attachments/assets/98902551-53be-4da6-8180-6ef14135a7e2" />

### Risk Areas:

#### Remote Access and Connectivity: 
- Legacy VPN provides limited access control and visibility for on-premises apps.
- Lack adaptive access controls and session visibility for Microsoft Entra ID- Integrated SaaS applications.

#### Data Storage and Protection:
- Relies on outdated file servers and tape libraries for sensitive data storage.
- Ransomware attack encrypted tape data, disrupting clinical trials.
- Increasing data volumes overwhelm existing achival workflows.

#### Regulatory Compliance and Incident Management: 
- Tape archival processes delay regulatory audits.
- Ransomware attack exposed compliance and vulnerability management weaknesses.
- Fragmented incident response increases resolution times.

#### Authentication and Authorization:
- External Researchers need seperate credentials for on premises access.
- Separation prevents consistent enforcement of Conditional Access and Multi Factor Authentication.
- Security Controls vary between cloud and on premises access.

### Threat Analysis:
1. Old VPNs give users too much trust once they get past the login screen. Modern security (like Zero Trust) fixes this by making you prove who you are at every single door inside the house, not just the front door.
2. The primary security risk of legacy tape-based backups is their lack of encryption and automated integrity checks, which leaves data vulnerable to theft and undetected tampering. While issues like slow transfer speeds and high maintenance costs are significant operational hassles, they do not create direct data security vulnerabilities like physical media vulnerabilities do.
3. (Fragmented governance), Organization lacks a centralized IT rulebook, causing different departments to manage their systems with disconnected rules. This disorganization makes it nearly impossible to guarantee that all infrastructure components meet strict legal standards everywhere. As a result, the primary risk is failing to follow mandatory regulatory laws consistently, which can lead to severe data protection failures or legal penalties.
4. Having disconnected identity systems prevents an organization from applying matching Multi-Factor Authentication and smart access rules across both cloud and physical environments. This lack of a unified defense creates weak spots, as hackers can exploit older, less-secure systems that do not benefit from modern cloud protections.

### Solutional Architecture:
#### Remote Access Modernization and Adaptive Access Control:
- Inbound Web App Security: Microsoft Entra Application Proxy securely publishes on-premises web applications to the cloud, allowing external participants and remote workers to connect using Single Sign-On (SSO) and MFA without opening inbound firewall ports.

- VPN Replacement: Microsoft Entra Private Access replaces traditional VPNs by providing secure, identity-based, granular access strictly to authorized internal resources, preventing risky lateral movement across the network.

- Central Control Engine: Microsoft Entra Conditional Access acts as the intelligent gatekeeper, enforcing real-time, adaptive security policies based on device compliance and user risk before any access is granted.

- Outbound Traffic Protection: Microsoft Entra Internet Access secures outbound traffic to the public internet and cloud-based SaaS apps by enforcing policy-based connectivity and data protection.

The architect dismantled the traditional network perimeter and successfully unified Contoso's hybrid infrastructure under a modern, centralized Zero Trust identity framework.

#### Ransomware resilience and backup protection:
- I decided to implement Azure Backup to instantly harden our infrastructure against ransomware by securing data in immutable vaults that cannot be altered or deleted by attackers. This architecture eliminates insider threats and administrative slip-ups by requiring multi-user authorization for critical deletions and providing a built-in soft-delete safety window for quick recovery. With automatic encryption ensuring our regulatory compliance and direct integration into Microsoft Defender and Azure Monitor, we gain an automated, centralized disaster recovery system that guarantees true business continuity.

#### Regulatory Compliance and Security Baseline Enforcement (HIPAA, HITRUST)

- I decided to implement Azure Arc, Azure Policy, and Microsoft Defender for Cloud because our hybrid infrastructure makes it incredibly difficult to measure and enforce strict healthcare standards like HIPAA and HITRUST across both our physical data center and cloud assets.

Here is exactly why I chose each of these tools to solve our compliance and security baseline challenges:

1. To bridge our hybrid infrastructure gap: I selected Azure Arc (with Guest Configuration) because we can't just secure the cloud; we have to enforce OS-level baselines, password policies, firewall rules, and audit settings on our physical on-premises servers as well.

2. To automate our regulatory guardrails: I chose Azure Policy because it allows me to deploy the built-in HIPAA and HITRUST 9.2 Regulatory Initiative frameworks directly. This automatically applies and enforces matching compliance rules across native cloud resources and our Arc-connected physical servers simultaneously.

3. To get audit-ready visibility: I chose Microsoft Defender for Cloud because my team needs a single pane of glass. Its Regulatory Compliance Dashboard constantly tracks our entire environment, visualizes our weak spots, and generates the reports we need to prove compliance to auditors.

#### Security Monitoring and Incident Response:

- I decided to implement Microsoft Sentinel, Microsoft Defender XDR, and Microsoft Security Copilot to drastically accelerate our detection, investigation, and response times across our hybrid workloads.

Here is why I chose this specific stack:

1. Microsoft Defender XDR: It automatically correlates signals across our endpoints, email, identity, and cloud infrastructure, allowing us to detect and stop advanced threats before they spread.

2. Microsoft Security Copilot: It leverages generative AI to automate threat hunting and immediately produce incident summaries, drastically reducing our investigation time.

3. Microsoft Sentinel: It centralizes our SIEM operations, using advanced incident correlation and automated response playbooks to instantly isolate threats across the entire enterprise.

### Final Architecture:

<img width="1010" height="614" alt="image" src="https://github.com/user-attachments/assets/fc0d7f91-057e-4367-95d8-a6f41c5bb2af" />


### Implementation:

#### Modernize remote access and enforce adaptive controls

- Deploy Microsoft Entra Private Access with GSA Connectors in the datacenter for secure, policy-driven access to on-premises apps and file servers.

- Replace legacy VPN access with GSA clients and per-app access policies.

- Publish internal web apps using Microsoft Entra Application Proxy with pre-authentication and MFA.

- Implement Microsoft Entra Internet Access to control outbound SaaS traffic with identity-based inspection.

- Define Conditional Access policies based on sign-in risk, device compliance, app sensitivity, and location.

#### Enhance ransomware resilience and backup protection

- Deploy Azure Backup to protect critical servers and data with immutable storage and soft-delete enabled.

- Enable multi-user authorization (MUA) for high-risk backup vault operations.

- Configure policy-based backup schedules and RPO targets aligned with business continuity needs.

- Integrate Azure Backup with Microsoft Defender for Cloud for security alerting and operational tracking.

- Use tape-to-cloud migration to transfer legacy tape backups to Azure and streamline archival workflows.

#### Enforce compliance and security baselines

- Connect on-premises servers to Azure using Azure Arc for centralized management and policy enforcement.

- Apply Azure Policy initiatives for HIPAA/HITRUST 9.2 compliance to Azure and Arc-connected resources.

- Configure Guest Configuration in Azure Arc to enforce OS-level baselines, including firewall, audit, and password policies.

- Continuously monitor compliance posture through the Microsoft Defender for Cloud Regulatory Compliance Dashboard.

#### Operationalize threat detection and incident response

- Deploy Microsoft Sentinel for SIEM capabilities and integrate with Microsoft Defender XDR for unified threat visibility.

- Create analytics rules for risky sign-ins, lateral movement, anomalous backup activity, and unauthorized access to clinical systems.

- Enable User and Entity Behavior Analytics (UEBA) and implement automated playbooks for critical incident response scenarios.

- Integrate Microsoft Security Copilot to support threat hunting, root cause analysis, and incident summarization using natural language.

#### Automate identity lifecycle and governance

- Implement Microsoft Entra Lifecycle Workflows to automate onboarding and offboarding for internal and external users.

- Use attribute-based assignment to trigger automatic group membership and access package provisioning.

- Pilot identity workflows in one research division and iterate before enterprise-wide rollout.

#### Govern external collaboration and resource access

- Design Access Packages with Entra Entitlement Management for external researchers and physicians.

- Apply multi-stage approval workflows, assignment expiration, and guest user access policies.

- Schedule recurring access reviews for all external identities and sensitive app groups.

- Monitor guest access lifecycle through audit logs and automate revocation of stale permissions.
