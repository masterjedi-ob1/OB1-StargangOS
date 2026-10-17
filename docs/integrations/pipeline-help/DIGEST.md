---

## id: OB1-GTM-PLH-GUIDE-DIGEST title: Pipeline guide for agents (skill.md). First full read and digest version: 1.0 source: [https\://app.pipeline.help/skill.md](https://app.pipeline.help/skill.md) (file header "Updated: 2026-10-13"), sha256 735ec64100a2323db3767bfe9ecf1e6f448f2ab138279a065ef117e44143e20c, 76,108 bytes companion\_source: [https\://app.pipeline.help/campaign-guide.md](https://app.pipeline.help/campaign-guide.md) (Updated 2026-10-09), sha256 cbdea15dc75478c3f6b7c7e50048ebfaa7dd5ca3f81955ff946db5a4984edad6 captured\_at: 2026-10-17T02:30Z exposure: E1 (no OB.1 internal names; safe for pipeline.help agents and the comms team) status: CONTEXT (vendor standard; vendor owns the source)

# Pipeline guide for agents: digest

Read as if new. The verbatim files sit in the repo bundle under kb/raw/pipeline-help/platform/. This page pulls out what an OB.1 operator or agent must know, and marks each point as a rule (the vendor's instruction), a capability, or a limit.

## 1\. What pipeline.help is, in the vendor's words

An AI agent team and shared workspace for B2B outreach and LinkedIn content. The external LLM reasons and writes; Pipeline saves evidence, builds tables, prepares campaigns, and runs native LinkedIn delivery through connected accounts.

## 2\. How to connect (capability)

- Hosted MCP: [https\://app.pipeline.help/api/mcp-server](https://app.pipeline.help/api/mcp-server), header "Authorization: Bearer "; personal tokens also send X-Pipeline-Workspace-Id.  
- CLI: npm install \-g pipeline-gtm@latest, then pipeline init, whoami, list-workspaces, config set defaultWorkspace. Use 1.3.3 or newer; 1.3.4+ self-updates (disable with PIPELINE\_AUTO\_UPDATE=0).  
- Discovery: MCP tools/list, resources/list, resources/read. CLI: pipeline run TOOL \--args '{...}' \--json.  
- References: /developers/api, /developers/mcp, /developers/cli, /developers/sdk, /openapi.json (212 paths), /campaign-guide.md.  
- Catalog: about 250 tools across 24 categories. Largest groups: Content 47, Agents 37, Enrichment Tables 20, Campaigns 17, Strategy 15\.

## 3\. The ten operating rules (rule)

1. Stay in the authorized workspace; verify identity before writes.  
2. Identify the exact target object; never silently pick the first or newest.  
3. Match requested scope; a connection-only request does not authorize scoring, follow-ups, withdrawal or InMail.  
4. Read schemas and skills; resolve providers by capability.  
5. Use your external LLM by default. Pipeline-hosted AI needs explicit consent. Never switch silently.  
6. Connected providers use workspace credentials; inspect limits before spending. No platform credit system.  
7. Save evidence with provenance (row IDs, versions, run IDs). Never invent contacts, facts, scores or outcomes.  
8. Pilot before scaling. Sending, publishing, destructive changes, CRM mutations and pushes need authorization. A draft is not approval.  
9. Keep async job and run IDs; after a timeout, check state before retrying a write.  
10. Report saved, skipped, failed, scheduled and sent work accurately. A create or start response is not proof of delivery.

These map one to one onto OB.1's Rules Before Tools doctrine and the G0/G1 gate chain. No conflict found.

## 4\. Task skills (capability)

pipeline://skill/ resources: onboard-workspace, build-campaign, build-enrichment-table, create-content, run-engagement, operate-gtm. Installable into Claude Code and Codex with "pipeline skills install \--targets claude-code,codex \--project .". These differ from the 83 workspace role skills and SOPs, which agents read with get-agent-skill-loadout and read-skill.

## 5\. Sourcing (rules)

- The seller's offer and the target audience are separate. Filters describe the audience's own business.  
- Before the first source call: read the loadout, list-architecture, the provider SOP and official provider filter docs. Record account criteria, person criteria, hard exclusions, effective filters, evidence checks and an approved canary ceiling.  
- Account-defined audiences: source-companies, qualify, then source-people with exact domains.  
- One bounded refinement per canary within budget; record before and after.  
- Exclusion QA: narrowest evidence-backed exclusion; never put negatives in include-only keywords; preserve removed rows; keep workspace suppressions intact.  
- Research mode: external agents use their own web search by default; a request to source from one provider does not authorize fallbacks to others.

## 6\. Agent Teams (capability and rules)

- Public roles: Strategist, GTM Engineer, Reply Agent, SDR Agent, GTM Lead, Content Agent. Internal stages: Scout, Researcher, ICP Gate, Writer, Closer, Coach.  
- External agents can claim, validate, submit or release work orders, and claim chat turns (10-minute lease).  
- Starting roles or messaging agents can invoke hosted AI; inspect consent first.

## 7\. Workflows (capability and limits)

Agent Workflows orchestrate sourcing, enrichment, tables, agents and destinations, separate from campaign delivery graphs. Plain-English compilation is hosted and needs consent. Graphs with hosted nodes need allowHostedAi=true. Never add a schedule just because a workflow was requested. Human trust and gate approvals are app-only, not MCP tools.

## 8\. Campaigns (rules)

- Machine creation needs an explicit workflow\_definition. Save draft, import, verify graph and sender.  
- ICP scoring, when used, must precede every sending path. Accepted and no-response branches must be explicit. Reply branches end the sequence. Withdrawal must never follow acceptance.  
- Render nested variables before import; blank or unresolved copy is a blocker.  
- Agent Teams launches use prepare-campaign-launch then launch-prepared-campaign, never start-campaign as a substitute. Pilot acceptance, scaling and launch are separate approvals.  
- add-prospects-bulk enrolls new prospects into an active campaign without restarting it.

## 9\. Signals and engagement (rules)

Engagement indicates attention, not buying intent. Read signal evidence before qualification. Comment drafting does not authorize posting; only regenerate uses hosted AI.

## 10\. Inbox, replies, SDR and CRM (rules and limits)

- Reply Agent handles new inbound replies; SDR handles warm threads that went quiet and stands down on any new reply.  
- analyze-sentiment and generate-reply-draft are hosted AI.  
- External Reply and SDR drafting saves pending Inbox drafts plus an internal CRM review task. Completion never authorizes sending, approval, booking or external CRM mutation.  
- External drafting must scope the Inbox owner, connected account and authorized conversation IDs. Never invent knowledge or widen scope to pass a readiness check.  
- Limit: external Reply Agent pickup "has passed one-time local scheduled Codex pickup; fresh production webhook delivery and permanent pickup remain rollout gates." Treat external reply automation as beta.  
- Connection acceptance arrives by delayed webhook or 15-minute polling; a sent request is not an acceptance.  
- "A reply does not automatically authorize an external CRM update."

## 11\. Content (rules)

Never invent the author's experiences, results or quotes. Keep company case studies separate from the author's personal record. Creator inspiration guides structure only. Publishing and scheduling need separate authorization.

## 12\. Analytics and improvement (rules)

Compare equivalent audiences and periods; never infer meetings or revenue from drafts. Use GTM Lead performance reviews to propose one clear experiment; preview revisions and refresh canary checks before applying. Accepting a coach action can trigger work.

## 13\. Blocklists and webhooks (rules)

Check exclusions before preparing audiences. Tests, redeliveries and outbound events call external systems and are not read-only. Secret rotation and endpoint deletion need authorization.

## 14\. What is new or decision-relevant for OB.1

| Item | Why it matters |
| :---- | :---- |
| Knowledge base and SOP drafts via API (save-knowledge-draft, publish-knowledge-draft, save-sop-draft, publish-sop-draft) | The empty Reply/SDR knowledge base can be authored by Kenobi from the E1 pack and published only on Chris's approval. This is the governed write path the KB plan assumed was unverified |
| save-onboarding-context (deterministic GTM Context write) | Loads the E1 GTM Context pack without hosted AI. Replaces hand entry |
| validate-campaign-brief, run-icp-canary-gate, preview-campaign-canary | Deterministic quality gates that match OB.1's G0 role |
| External Reply/SDR drafting with claim tokens | Lets an OB.1 seat draft replies with OB.1's own writing skill while pipeline.help holds the approval queue. Beta per the vendor |
| list-webhook-event-types, test-webhook-endpoint, list-webhook-deliveries | Diagnose the ob-sync receiver that has never received a delivery |
| add-to-blocklist with domains | Suppression for clients, partners and investors before any audience build |
| list-brief-metrics, get-mission-control-stats, get-agent-spend | Feeds for the StarGang GTM Scorecard Layers 2 and 4 |
| Guide is versioned by date in the file header | Re-read and diff on each re-baseline; store the hash |

