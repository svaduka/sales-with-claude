# lev-questions-checking

# Meeting Summary: RFP Clarifications and Estimation Impact Alignment
Date and Time: 2026-04-14, 13:51
Participants:
- Speaker 1 (Solution Architect)
- Speaker 2 (Pre-Sales/Proposal Lead; referred to as “lev” at closing)
Summary of the Meeting:
- The meeting focused on refining the scope and nature of questions to send to the customer for an RFP related to an “enterprise ARK control panel” on AWS.
- Speaker 2 emphasized that all clarifying questions must directly impact pre-sales deliverables: cost, duration, team composition, and high-level architecture. Questions relevant only to delivery should be deferred.
- Speaker 1 outlined several architectural and integration uncertainties (cloud provider, AWS architectural pattern, scalability metrics, multi-tenancy, disaster recovery, integrations with nine systems, data quality, compliance, region constraints, and vendor coordination), and sought confirmation that these are aligned to estimation needs.
- The team agreed to prioritize questions that influence timeline, team composition, and the feasibility of the proposed architecture (e.g., acceptable Bedrock models vs. external integrations).
- Action: Speaker 1 will consolidate RFP-impacting clarifications and share a focused document tailored to pre-sales estimation.
## Topic 1: Architectural Direction and Cloud Provider Assumptions (AWS)
- Speaker 1: “What is the preferred cloud provider… I mention it as AWS.”
  - Assumes AWS as the provider for the enterprise ARK control panel.
- Speaker 1: Raised target AWS architecture pattern questions (serverless vs. containers) and scalability signals (concurrent users, requests per second, document volumes by vendor).
  - Noted gaps that affect capacity planning, sizing, and hence estimates.
- Speaker 2: “The questions that we are asking at this point is something that needs to be helping us to estimate… and come up with the architectural approach… at the stage of the proposal.”
  - Reinforced relevance filter: only ask questions that change cost/duration/team.
- Decisions:
  - Proceed with AWS as the working assumption but request confirmation from the client.
  - Collect minimal metrics needed for sizing (concurrency, RPS, doc volumes) because they impact timelines and composition.
- Challenges:
  - Missing scalability data and architecture preferences make it hard to produce a realistic cost and duration.
- Planned Actions:
  - Speaker 1 to frame the architecture questions narrowly to estimation impact.
Action Items
- Clarify cloud provider (AWS) confirmation
  - Description: Request explicit confirmation of AWS as the mandated provider.
  - Responsible: Speaker 1
  - Time Frame: 2 business days
  - Due Date: 2026-04-16
  - Notes: Impacts solution assumptions and pricing models.
- Request target AWS architecture pattern (serverless vs. containers)
  - Description: Ask for preferences or constraints on serverless vs. containerized approaches.
  - Responsible: Speaker 1
  - Time Frame: 2 business days
  - Due Date: 2026-04-16
  - Notes: Impacts cost model, team skills, and delivery approach.
- Gather scalability metrics
  - Description: Request expected concurrent users, RPS, and document volumes per vendor.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Required for capacity estimates and cost modeling.
Open Questions
- What AWS architectural pattern does the client prefer (serverless, containers, hybrid)?
- What are the target scalability metrics (concurrency, throughput, volumes)?
- Are there constraints that would prohibit certain AWS managed services?
## Topic 2: Pre-Sales Focus on Estimation-Impacting Questions
- Speaker 2: “We are on pre-sales… the questions that we ask must be the ones that actually impact our proposal.”
  - Clear guidance to avoid delivery-only details (UI minutiae, deep operational concerns).
- Speaker 2: “EPAM is going to… propose resource plan, project plan, milestones… Or we will say there is no bloody way to do it in this timeframe.”
  - Indicates willingness to challenge unrealistic client timelines and provide a justified alternative.
- Speaker 1: “This is just an RFP… at least minimum things are required… to understand our timeline and everything.”
  - Agrees and refocuses on estimation-critical clarifications.
- Decisions:
  - Filter the question set to only estimation-impacting items.
- Challenges:
  - Balancing comprehensiveness with pre-sales constraints.
- Planned Actions:
  - Speaker 1 will produce a concise clarification list aligned to cost/duration/team composition.
Action Items
- Curate estimation-impacting question set
  - Description: Review and refine the question list to only those affecting cost, duration, team, and high-level architecture.
  - Responsible: Speaker 1
  - Time Frame: 2 business days
  - Due Date: 2026-04-16
  - Notes: Defers delivery-only questions to later phases.
- Prepare alternative timeline proposal
  - Description: Draft realistic project plan and milestones to counter unrealistic client timelines if needed.
  - Responsible: Speaker 2
  - Time Frame: 5 business days
  - Due Date: 2026-04-21
  - Notes: Include assumptions and risks; align with capacity data once received.
Open Questions
- Which client timeline constraints are fixed vs. negotiable?
- What criteria will the client use to accept an alternative schedule?
## Topic 3: Delivery Timelines and Team Composition
- Speaker 1: “They mentioned… the first lot… deliver it in the one month… You want to check on that delivery timelines?”
- Speaker 2: “They have this delivery approach… resource plan… EPAM is going to… say… here is our resource plan… or we will say there is no bloody way to do it in this timeframe.”
  - EPAM will provide its own plan and challenge if necessary.
- Speaker 1 and Speaker 2: Alignment that timeline and team composition must be derived from architectural and integration realities.
- Decisions:
  - EPAM to propose an independent plan with milestones, team composition, and cost.
- Challenges:
  - Unclear inputs (integration scope, volumes) may make a one-month “first lot” unrealistic.
- Planned Actions:
  - Gather data needed to judge feasibility; prepare an alternative if needed.
Action Items
- Validate feasibility of “first lot in one month”
  - Description: Assess whether initial delivery within one month is achievable given current unknowns.
  - Responsible: Speaker 2, with input from Speaker 1
  - Time Frame: 5 business days
  - Due Date: 2026-04-21
  - Notes: Depends on integration scope and volumes.
- Draft team composition proposal
  - Description: Propose team roles and sizes based on likely architecture (serverless/containers) and integration needs.
  - Responsible: Speaker 2
  - Time Frame: 5 business days
  - Due Date: 2026-04-21
  - Notes: Adjust after receiving client clarifications.
Open Questions
- What are the exact milestones expected in “Lot A” and “Lot B1–B7”?
- Are partial deliverables acceptable within the first month?
## Topic 4: Integration Scope and “Nine Systems”
- Speaker 1: “They mentioned nine systems also… what are those nine systems?… How the integration model works… they haven’t mentioned anything… That will impact our timelines too.”
  - Integration complexity is unknown and directly affects estimates.
- Speaker 1: Will include integration clarification in the RFP question set.
- Decisions:
  - Request detailed list of systems, integration patterns, protocols, authentication, and expected data exchange volumes.
- Challenges:
  - Without integration detail, SOW and effort estimates may be inaccurate.
- Planned Actions:
  - Prioritize integration questions due to strong estimation impact.
Action Items
- Obtain detailed list of “nine systems”
  - Description: Request system names, owners, interfaces (APIs, file drops), auth methods, SLAs.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Needed for effort sizing and risk analysis.
- Request integration model details
  - Description: Clarify messaging patterns (sync/async), data formats, transport protocols, and error handling expectations.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Impacts architecture choice and timelines.
Open Questions
- What are the nine systems and their integration readiness?
- Are there existing integration hubs or ESBs in use?
- Are there vendor-specific constraints for each system?
## Topic 5: Data Quality and Document Extraction Requirements
- Speaker 1: “They want to… extract the document… what is the data quality things?… we don’t know anything on that.”
  - Data quality variability impacts model selection, validation processes, rework rates, and delivery time.
- Speaker 1: Plans to summarize questions on data quality for the RFP.
- Decisions:
  - Ask for document types, formats, OCR needs, expected error rates, labeling standards, and acceptance criteria.
- Challenges:
  - Unknown data quality can significantly change effort (e.g., preprocessing, validation workflows).
- Planned Actions:
  - Include focused data quality questions that affect scope and duration.
Action Items
- Request document taxonomy and quality metrics
  - Description: Ask for types (invoices, forms), formats (PDF, images), scan quality, language, and expected accuracy thresholds.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Impacts model selection and QA processes.
- Clarify acceptance criteria for extraction
  - Description: Define accuracy thresholds, validation workflows, and reprocessing policies.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Influences timeline and staffing (QA/annotation).
Open Questions
- What are the mandatory accuracy thresholds per document type?
- Will there be human-in-the-loop validation, and at what scale?
## Topic 6: Compliance (GDPR, AI, EU, Vendor-Specific)
- Speaker 1: “They’re also asking us compliance… GDPR… AI compliance and EU compliance… AI is different for different region… we don’t know anything particular to the ethenic [ethica?].”
  - Compliance scope unclear; may constrain model choices, data residency, and vendor selection.
- Decisions:
  - Request specific compliance frameworks and certifications required; confirm regional legal constraints.
- Challenges:
  - Compliance differences can impact feasible services (e.g., model availability, logging policies) and therefore timeline.
- Planned Actions:
  - Include compliance clarifications focused on estimation impact (data residency, audit needs, approved services).
Action Items
- Enumerate required compliance standards
  - Description: Ask for exact frameworks (e.g., GDPR articles, EU AI Act positions, vendor-specific policies), required certs.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Impacts architecture choices and documentation effort.
- Confirm data residency and processing constraints
  - Description: Validate region restrictions and cross-border data flow policies.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Aligns with AWS region selection and service availability.
Open Questions
- Which AI compliance standards apply and how do they constrain model/service choices?
- Are there audit logging and retention requirements that affect design?
## Topic 7: AWS Bedrock Models vs. External Services
- Speaker 2: “Like the question you’re asking which Bedrock models are acceptable… how will it… impact our estimates…?”
  - Challenges the necessity unless it impacts integration complexity and timelines.
- Speaker 1: “If it is only Bedrock… timeline will be straight… But if it is an open search or anything external… we need to think about how the integration will work… That will impact our project timeline.”
  - Argues model/service selection has tangible integration impact.
- Decisions:
  - Keep questions that differentiate between native AWS services (Bedrock) vs. external vendors, as they alter integration scope.
- Challenges:
  - Model availability and compliance constraints may limit choices within certain regions.
- Planned Actions:
  - Ask for approved model/services list and any prohibitions.
Action Items
- Request approved/acceptable LLMs and services
  - Description: Ask if AWS Bedrock models (e.g., Titan, Llama) are permitted; clarify any disallowed models/services.
  - Responsible: Speaker 1
  - Time Frame: 2 business days
  - Due Date: 2026-04-16
  - Notes: Impacts integration and compliance alignment.
- Identify external integration constraints
  - Description: Determine if non-AWS services are allowed and what security/compliance steps are required.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Influences effort sizing and risk.
Open Questions
- Which specific Bedrock models are approved?
- Are there prohibitions on using non-AWS AI services?
## Topic 8: Region Constraints and Delivery Management Boundaries
- Speaker 1: “Region wise they mention EU region… in Abu Dhabi… within the region… they are only looking for their own region… they don’t access.”
  - Raises concerns about strict region residency constraints.
- Speaker 2: “Luckily that’s the issue of delivery management… you as a solution architect should not be bothered with matters like can we hire from Romania… Greece… Cyprus.”
  - Separates staffing and hiring constraints from solution architecture.
- Decisions:
  - Limit questions to architectural impacts (data residency, service availability) and avoid staffing geography questions in pre-sales clarifications.
- Challenges:
  - Need to ensure region constraints are captured without drifting into delivery management concerns.
- Planned Actions:
  - Include region/data residency questions; exclude hiring geography concerns.
Action Items
- Confirm AWS EU region usage and data residency rules
  - Description: Ask which EU regions are permissible and whether data must remain in a specific country.
  - Responsible: Speaker 1
  - Time Frame: 2 business days
  - Due Date: 2026-04-16
  - Notes: Impacts service selection and architecture.
- Exclude staffing geography from RFP clarifications
  - Description: Remove or defer questions related to hiring locations; handle via delivery management.
  - Responsible: Speaker 1
  - Time Frame: Immediate
  - Due Date: 2026-04-14
  - Notes: Aligns with pre-sales focus.
Open Questions
- Are there country-specific restrictions within the EU (e.g., data stay-in-country)?
- Does the client require sovereign cloud controls?
## Topic 9: Multi-Tenancy and Disaster Recovery (DR)
- Speaker 1: “Multiple vendors… is there any multi-tenancy approaches required? Or it’s a single tenant… They haven’t mentioned anything related to disaster recovery.”
  - Tenancy model and DR strategy have significant architectural and effort implications.
- Decisions:
  - Ask directly about tenancy requirements and DR RTO/RPO.
- Challenges:
  - DR expectations can change environment count, replication strategy, and cost; tenancy affects isolation and complexity.
- Planned Actions:
  - Include targeted tenancy and DR questions.
Action Items
- Confirm tenancy model
  - Description: Clarify whether single-tenant or multi-tenant architecture is required and isolation expectations.
  - Responsible: Speaker 1
  - Time Frame: 2 business days
  - Due Date: 2026-04-16
  - Notes: Impacts design complexity and cost.
- Define DR requirements
  - Description: Request RTO/RPO targets, failover regions, backup, and recovery testing expectations.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Influences environment design and timelines.
Open Questions
- What RTO/RPO does the client require?
- Is cross-region DR acceptable within EU constraints?
## Topic 10: Vendor Coordination Across Lots (Lot A; Lot B1–B7)
- Speaker 1: “They mentioned… lot A and lot B1 to 7… multiple vendors can also work… how that coordination will happen.”
  - Coordination affects integration sequencing, dependencies, and milestone commitments.
- Speaker 2: “Go ahead, shoot your shot… many thanks.”
  - Encourages including coordination clarifications that impact plan feasibility.
- Decisions:
  - Ask for governance model, ownership per lot, integration sequencing, and escalation paths.
- Challenges:
  - Without coordination clarity, risk of delays and misaligned milestones.
- Planned Actions:
  - Include vendor coordination questions that map to dependencies and schedule risks.
Action Items
- Request multi-vendor governance details
  - Description: Ask for roles, decision forums, change control, and integration ownership per lot.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Impacts risk planning and schedule.
- Clarify dependency mapping across lots
  - Description: Obtain a dependency matrix and milestone alignment across vendors.
  - Responsible: Speaker 1
  - Time Frame: 3 business days
  - Due Date: 2026-04-17
  - Notes: Affects feasibility of proposed timelines.
Open Questions
- Who is the lead integrator or PMO across vendors?
- What are the escalation and decision-making mechanisms?
## Topic 11: Next Steps and Deliverables
- Speaker 1: “I will… send that… I will provide this one… only particularly to RFP.”
  - Commits to sharing the refined clarification document.
- Speaker 2: “Just keep it in mind, my guidance… doing great.”
  - Confirms alignment and encourages proceeding.
- Decisions:
  - Proceed with compiling and sending RFP-focused clarifications.
- Challenges:
  - Ensuring no non-impact questions slip into the pre-sales clarification set.
- Planned Actions:
  - Share the clarification list; prepare proposal with alternative timelines if necessary.
Action Items
- Send refined RFP clarification document
  - Description: Deliver the filtered list of questions focused on estimation impact.
  - Responsible: Speaker 1
  - Time Frame: 2 business days
  - Due Date: 2026-04-16
  - Notes: Include architecture, integration, data quality, compliance, region, and coordination items.
- Prepare proposal draft (cost, duration, team, milestones)
  - Description: Draft proposal reflecting assumptions; include an alternative timeframe if client’s is unrealistic.
  - Responsible: Speaker 2
  - Time Frame: 5 business days
  - Due Date: 2026-04-21
  - Notes: Reference clarifications or note assumptions where answers are pending.
Open Questions
- Are there any hard deadlines from the client beyond the “first lot” mention?
- Will there be a formal Q&A window for RFP clarifications?
Generated by gpt-5