Digest: see [DIGEST.md](DIGEST.md) (OB1-GTM-PLH-GUIDE-DIGEST v1.0)

# pipeline.help agent guide

- **Source:** https://app.pipeline.help/developers/api
- **Pasted by:** Chris on 2026-10-16
- **Owner:** Galactic_Grok_OB1 (GTM / pipeline turf)

## OB.1 guardrails

Attio stays the CRM of record. pipeline.help CRM ops are not the source of truth for people, companies, or deals.

These need Chris's approval before you run them: `send-message`, any `publish-*`, any `activate-*`, `apply-campaign-revision`, `push-outbound-event`, any `delete-*`, and `accept-coach-action`. They are outside sends or irreversible actions.

Reads, `dry-run-skill`, and drafts are fine without that approval.

---

### Inbox

| Operation | Purpose |
| --- | --- |
| [`analyze-sentiment`](https://app.pipeline.help/developers/api?operation=analyze-sentiment) | Run the SentimentAgent on a conversation: classifies the prospect across the canonical 7 stages (initial, interested, neutral, objection, meeting_ready, closed_lost, closed_won) and updates the conversation_contexts row |
| [`generate-reply-draft`](https://app.pipeline.help/developers/api?operation=generate-reply-draft) | Run the ReplyAgent to draft a reply to an inbox conversation, using workspace GTM context (offers, ICP, personas, case studies) and calendar availability |

### Search

| Operation | Purpose |
| --- | --- |
| [`resolve-linkedin-search-parameters`](https://app.pipeline.help/developers/api?operation=resolve-linkedin-search-parameters) | Resolve human-readable LinkedIn location, industry, company, school, function, or seniority labels to provider IDs before searching |
| [`search-people-database`](https://app.pipeline.help/developers/api?operation=search-people-database) | LinkedIn people search through a connected account |
| [`search-companies-database`](https://app.pipeline.help/developers/api?operation=search-companies-database) | LinkedIn company search through a connected account |
| [`source-people`](https://app.pipeline.help/developers/api?operation=source-people) | Source people from the best connected workspace prospect database |
| [`source-companies`](https://app.pipeline.help/developers/api?operation=source-companies) | Source companies from the best connected workspace account database |
| [`list-sales-navigator-sources`](https://app.pipeline.help/developers/api?operation=list-sales-navigator-sources) | List the saved searches, saved lead lists, and saved account lists available to a connected Sales Navigator account |
| [`pull-sales-navigator-lead-list`](https://app.pipeline.help/developers/api?operation=pull-sales-navigator-lead-list) | Pull people from a discovered Sales Navigator saved lead list by ID or URL |

### Workspaces

| Operation | Purpose |
| --- | --- |
| [`get-ai-settings`](https://app.pipeline.help/developers/api?operation=get-ai-settings) | Read workspace AI defaults, independent tool-calling model, and JEV decision routing. |
| [`update-ai-settings`](https://app.pipeline.help/developers/api?operation=update-ai-settings) | Update workspace AI settings |
| [`list-ai-decisions`](https://app.pipeline.help/developers/api?operation=list-ai-decisions) | Read the last 50 decision calls, including confidence, provider, usage, cost, and failures |
| [`scrape-website`](https://app.pipeline.help/developers/api?operation=scrape-website) | Pipeline recommended website scraping via workspace Spider.cloud BYOK |
| [`list-workspaces`](https://app.pipeline.help/developers/api?operation=list-workspaces) | List every workspace the authenticated account can currently access, including each workspace ID, slug, ownership state, and live permissions |
| [`get-workspace`](https://app.pipeline.help/developers/api?operation=get-workspace) | Get workspace information. |
| [`create-workspace`](https://app.pipeline.help/developers/api?operation=create-workspace) | Create a workspace for the authenticated personal-token owner after the same subscription checks as the UI |
| [`delete-workspace`](https://app.pipeline.help/developers/api?operation=delete-workspace) | Permanently delete one exact workspace owned by the authenticated personal-token user |
| [`get-workspace-subscription`](https://app.pipeline.help/developers/api?operation=get-workspace-subscription) | Get the workspace owner's subscription state in one call: planType (starter/pro/etc), status, isAdmin, trialEnd, trialDaysRemaining, isTrialActive, totalSeats, usedSeats, and currentPeriodEnd |
| [`list-integrations`](https://app.pipeline.help/developers/api?operation=list-integrations) | List BYOK integration credentials stored for the workspace (Instantly, SmartLead, HubSpot, Attio, Tavily, Exa, Firecrawl, Prospeo, and other supported services) |
| [`create-integration-credential`](https://app.pipeline.help/developers/api?operation=create-integration-credential) | Store a BYOK integration credential for the workspace (bring your own API key/token) |
| [`delete-integration-credential`](https://app.pipeline.help/developers/api?operation=delete-integration-credential) | Permanently remove one exact BYOK integration credential from the authenticated workspace |

### Webhooks

| Operation | Purpose |
| --- | --- |
| [`list-webhook-event-types`](https://app.pipeline.help/developers/api?operation=list-webhook-event-types) | List the outbound Pipeline webhook events available to the workspace, including stable keys, groups, descriptions, API versions, campaign-filter support, and example payloads. |
| [`list-webhook-endpoints`](https://app.pipeline.help/developers/api?operation=list-webhook-endpoints) | List outbound webhook endpoints in the workspace, including subscriptions, filters, status, health, and recent delivery state |
| [`create-webhook-endpoint`](https://app.pipeline.help/developers/api?operation=create-webhook-endpoint) | Create an HTTPS webhook endpoint with explicit event subscriptions and optional campaign filters and destination authentication |
| [`get-webhook-endpoint`](https://app.pipeline.help/developers/api?operation=get-webhook-endpoint) | Get one outbound webhook endpoint by ID |
| [`update-webhook-endpoint`](https://app.pipeline.help/developers/api?operation=update-webhook-endpoint) | Update an outbound webhook endpoint, its explicit subscriptions, filters, destination authentication, or active and paused status. |
| [`delete-webhook-endpoint`](https://app.pipeline.help/developers/api?operation=delete-webhook-endpoint) | Delete an outbound webhook endpoint and cancel work that has not started. |
| [`test-webhook-endpoint`](https://app.pipeline.help/developers/api?operation=test-webhook-endpoint) | Send one signed test delivery through the endpoint delivery path |
| [`rotate-webhook-secret`](https://app.pipeline.help/developers/api?operation=rotate-webhook-secret) | Rotate an endpoint signing secret |
| [`list-webhook-deliveries`](https://app.pipeline.help/developers/api?operation=list-webhook-deliveries) | List a cursor-paginated delivery history for an endpoint, with optional event, status, and date filters |
| [`redeliver-webhook-delivery`](https://app.pipeline.help/developers/api?operation=redeliver-webhook-delivery) | Redeliver a retained delivered or exhausted webhook event using its original event ID and immutable body |

### CRM / Pipeline

| Operation | Purpose |
| --- | --- |
| [`get-crm-pipeline`](https://app.pipeline.help/developers/api?operation=get-crm-pipeline) | Get the workspace CRM kanban: prospects grouped by conversionStage (connected, replied, interested, meeting_request, qualified, meeting_scheduled, meeting_completed, won, lost, not_interested, unqualified) |
| [`move-prospect-stage`](https://app.pipeline.help/developers/api?operation=move-prospect-stage) | Move a prospect along the CRM funnel by setting their conversionStage |
| [`add-prospect-note`](https://app.pipeline.help/developers/api?operation=add-prospect-note) | Add a note to a prospect. |
| [`update-prospect-tags`](https://app.pipeline.help/developers/api?operation=update-prospect-tags) | Add/remove custom tags |
| [`list-crm-tasks`](https://app.pipeline.help/developers/api?operation=list-crm-tasks) | Read canonical tasks |
| [`create-crm-task`](https://app.pipeline.help/developers/api?operation=create-crm-task) | Create a task without sending |
| [`update-crm-task`](https://app.pipeline.help/developers/api?operation=update-crm-task) | Edit, complete or reopen a task |
| [`list-prospect-activities`](https://app.pipeline.help/developers/api?operation=list-prospect-activities) | Read activity with trusted actor provenance |

### ICP / GTM

| Operation | Purpose |
| --- | --- |
| [`get-icp-profile`](https://app.pipeline.help/developers/api?operation=get-icp-profile) | Get the ICP profile for a workspace. |
| [`get-gtm-context`](https://app.pipeline.help/developers/api?operation=get-gtm-context) | Read the workspace's full GTM context: personas, commercial offerings, campaign offers, canonical lead magnets, case studies, competitors, ICP criteria, company/service descriptions, and onboarding evidence keyed to the canonical saved asset IDs |
| [`get-onboarding-readiness`](https://app.pipeline.help/developers/api?operation=get-onboarding-readiness) | Inspect connected website-search, LinkedIn, lead-source, email-finder, and optional hosted-LLM capabilities |
| [`save-onboarding-context`](https://app.pipeline.help/developers/api?operation=save-onboarding-context) | Validate and deterministically persist a coding-agent-authored onboarding artifact into the GTM context, default ICP, personas, offerings, case studies, and competitors used by Launchpad |
| [`score-prospect`](https://app.pipeline.help/developers/api?operation=score-prospect) | Score a prospect against the workspace ICP. |
| [`set-icp-profile`](https://app.pipeline.help/developers/api?operation=set-icp-profile) | Create or update the workspace's ICP profile (inferred from auth, no workspaceId needed) |
| [`list-segments`](https://app.pipeline.help/developers/api?operation=list-segments) | List the workspace GTM segments available in Launchpad so the operator can choose an exact segment before creating or reusing a campaign brief |
| [`create-segment`](https://app.pipeline.help/developers/api?operation=create-segment) | Generate GTM buyer segments from company context using the workspace's BYOK LLM and persist them as draft segments |
| [`save-segment`](https://app.pipeline.help/developers/api?operation=save-segment) | Deterministically create or update one coding-agent-authored Launchpad segment by workspace and slug |
| [`update-segment`](https://app.pipeline.help/developers/api?operation=update-segment) | Patch selected fields on one draft Launchpad segment |
| [`activate-segment-pilot`](https://app.pipeline.help/developers/api?operation=activate-segment-pilot) | Activate one explicitly selected Launchpad segment |
| [`run-onboarding`](https://app.pipeline.help/developers/api?operation=run-onboarding) | Analyze a company website (server-side Tavily + Anthropic research, ICP-onboarding path only) to bootstrap GTM setup: service description, ICP summary, target titles/industries, primary/secondary personas, case study summaries, and a default offer/lead magnet suggestion |

### Blocklist

| Operation | Purpose |
| --- | --- |
| [`list-blocklist`](https://app.pipeline.help/developers/api?operation=list-blocklist) | List blocked domains and profiles. |
| [`add-to-blocklist`](https://app.pipeline.help/developers/api?operation=add-to-blocklist) | Add a domain or profile to the blocklist. |
| [`check-blocklist`](https://app.pipeline.help/developers/api?operation=check-blocklist) | Check if a domain or profile is blocklisted. |

### Async Jobs

| Operation | Purpose |
| --- | --- |
| [`get-job`](https://app.pipeline.help/developers/api?operation=get-job) | Poll the status of an async MCP job |
| [`cancel-job`](https://app.pipeline.help/developers/api?operation=cancel-job) | Cancel a running async MCP job. |

### Messaging

| Operation | Purpose |
| --- | --- |
| [`send-message`](https://app.pipeline.help/developers/api?operation=send-message) | Send a LinkedIn message in a conversation |

### Agents

| Operation | Purpose |
| --- | --- |
| [`list-agent-chats`](https://app.pipeline.help/developers/api?operation=list-agent-chats) | List your private Agent Teams chats and settings |
| [`get-agent-chat`](https://app.pipeline.help/developers/api?operation=get-agent-chat) | Read your private Agent Teams chat messages, turn status and live results |
| [`send-agent-chat-message`](https://app.pipeline.help/developers/api?operation=send-agent-chat-message) | Attach bounded page IDs with surfaceContext for contextual work |
| [`claim-agent-chat-turn`](https://app.pipeline.help/developers/api?operation=claim-agent-chat-turn) | Claim an external Agent Teams chat turn for ten minutes |
| [`complete-agent-chat-turn`](https://app.pipeline.help/developers/api?operation=complete-agent-chat-turn) | Save your coding-agent-authored response as the addressed agent in its private chat, complete the leased external turn, and return any parent continuation |
| [`delegate-agent-chat-turn`](https://app.pipeline.help/developers/api?operation=delegate-agent-chat-turn) | Delegate a claimed external chat task to another public Pipeline agent with originating conversation context and scope |
| [`update-agent-chat-settings`](https://app.pipeline.help/developers/api?operation=update-agent-chat-settings) | Update your private Agent Teams chat identity, model preferences and opted-in routines with revision conflict protection |
| [`list-agents-status`](https://app.pipeline.help/developers/api?operation=list-agents-status) | List the current state of the Pipeline agent team and the GTM Engineer internal stages: autonomy setting, schedule, daily cap, active skills, and the last run summary |
| [`list-recent-agent-runs`](https://app.pipeline.help/developers/api?operation=list-recent-agent-runs) | Paginated activity log of recent agent wake-ups in the workspace |
| [`get-agent-run`](https://app.pipeline.help/developers/api?operation=get-agent-run) | Drill into a specific agent run: full input/output summary plus every tool call (agent_run_steps) with its arguments, output, duration, and tokens |
| [`list-workspace-skills`](https://app.pipeline.help/developers/api?operation=list-workspace-skills) | List Pipeline-owned first-party skills available in the workspace |
| [`get-agent-skill-loadout`](https://app.pipeline.help/developers/api?operation=get-agent-skill-loadout) | Resolve the effective role and task skill loadout for an external coding agent, including workspace overlays, provider SOPs, versions, hashes, required context, and MCP resource URIs |
| [`get-agent-setup`](https://app.pipeline.help/developers/api?operation=get-agent-setup) | Read Reply Agent, SDR Agent and Content Agent setup readiness before using them |
| [`get-sop-context`](https://app.pipeline.help/developers/api?operation=get-sop-context) | Read Reply/SDR base SOP, full GTM context, active overlay and pending draft |
| [`get-knowledge-base`](https://app.pipeline.help/developers/api?operation=get-knowledge-base) | Read shared Reply/SDR knowledge, active version, pending draft and GTM context |
| [`save-knowledge-draft`](https://app.pipeline.help/developers/api?operation=save-knowledge-draft) | Save the full merged knowledge object as an inactive draft |
| [`publish-knowledge-draft`](https://app.pipeline.help/developers/api?operation=publish-knowledge-draft) | Publish the exact reviewed knowledge draft only after explicit user approval, using the returned draft timestamp |
| [`save-sop-draft`](https://app.pipeline.help/developers/api?operation=save-sop-draft) | Save a personalized Reply/SDR SOP as an inactive versioned workspace draft |
| [`publish-sop-draft`](https://app.pipeline.help/developers/api?operation=publish-sop-draft) | Publish the exact reviewed SOP draft after explicit user approval |
| [`read-skill`](https://app.pipeline.help/developers/api?operation=read-skill) | Read the full playbook body of one Pipeline-owned first-party workspace skill by name |
| [`read-provider-docs`](https://app.pipeline.help/developers/api?operation=read-provider-docs) | Read current official provider documentation or live GetLeads MCP tool schemas using the connected workspace credential |
| [`search-quickenrich`](https://app.pipeline.help/developers/api?operation=search-quickenrich) | Search connected QuickEnrich company or contact discovery with native documented include/exclude filters |
| [`get-coach-briefing`](https://app.pipeline.help/developers/api?operation=get-coach-briefing) | Read the latest Coach digest: the workspace-scoped learned_context that Coach writes after each daily synthesis |
| [`get-coach-performance-reviews`](https://app.pipeline.help/developers/api?operation=get-coach-performance-reviews) | Read the GTM Lead performance-review model, including the current diagnosis, experiments, retained learnings, backlog, or weekly history |
| [`run-skill`](https://app.pipeline.help/developers/api?operation=run-skill) | Run a Pipeline-owned first-party skill through Pipeline hosted inference |
| [`dry-run-skill`](https://app.pipeline.help/developers/api?operation=dry-run-skill) | Simulate what an agent would do without executing any side effects |
| [`list-agent-work-orders`](https://app.pipeline.help/developers/api?operation=list-agent-work-orders) | List Agent Teams work orders that an external coding agent can claim |
| [`claim-agent-work-order`](https://app.pipeline.help/developers/api?operation=claim-agent-work-order) | Lease one claimable Agent Teams work order for execution inside an external coding agent |
| [`validate-agent-artifact`](https://app.pipeline.help/developers/api?operation=validate-agent-artifact) | Validate an external coding agent artifact against the exact typed Agent Teams output contract before submission |
| [`submit-agent-artifact`](https://app.pipeline.help/developers/api?operation=submit-agent-artifact) | Submit a validated external coding agent artifact to its claimed Agent Teams work order |
| [`release-agent-work-order`](https://app.pipeline.help/developers/api?operation=release-agent-work-order) | Release an external coding agent work-order lease without submitting an artifact |
| [`list-handoffs`](https://app.pipeline.help/developers/api?operation=list-handoffs) | Read the live agent handoff queue (Scout to Researcher, Researcher to ICP, etc) |
| [`get-agent-spend`](https://app.pipeline.help/developers/api?operation=get-agent-spend) | LLM spend for the agent assembly line |
| [`get-icp-funnel`](https://app.pipeline.help/developers/api?operation=get-icp-funnel) | ICP gate funnel counts for the workspace: unscored, scoring, qualified, priority, disqualified, and number passing downstream |
| [`get-mission-control-stats`](https://app.pipeline.help/developers/api?operation=get-mission-control-stats) | Workspace agent-team rollup |
| [`accept-coach-action`](https://app.pipeline.help/developers/api?operation=accept-coach-action) | Execute a Coach recommendation |
| [`trigger-agent-role`](https://app.pipeline.help/developers/api?operation=trigger-agent-role) | Create a work order for one Agent Teams role |

### Approvals

| Operation | Purpose |
| --- | --- |
| [`list-pending-approvals`](https://app.pipeline.help/developers/api?operation=list-pending-approvals) | List human-input items awaiting approval across the workspace: draft sends, drafted replies, push events, and Agent Teams human-input cards |
| [`get-approval-detail`](https://app.pipeline.help/developers/api?operation=get-approval-detail) | Drill into one approval item |
| [`resolve-reply-draft`](https://app.pipeline.help/developers/api?operation=resolve-reply-draft) | Approve or reject one pending Reply Agent draft by id |
| [`resolve-hitl-card`](https://app.pipeline.help/developers/api?operation=resolve-hitl-card) | Resolve an Agent Teams human-input card |
| [`push-outbound-event`](https://app.pipeline.help/developers/api?operation=push-outbound-event) | Mark a pending push event as pushed after approval |

### Strategy

| Operation | Purpose |
| --- | --- |
| [`get-strategy-snapshot`](https://app.pipeline.help/developers/api?operation=get-strategy-snapshot) | Preflight distillation of your GTM context into a compact, high-signal strategy snapshot: best ICP, commercial offerings, campaign offers, lead magnets, the only valid proof points (case studies), banned phrases, and the channels the Strategist may plan |
| [`create-strategy-ideas`](https://app.pipeline.help/developers/api?operation=create-strategy-ideas) | Run the Strategist diverge pass: brainstorm and curate campaign ideas (hook angle, archetype, personalization elements, CTA, proof point, differentiation, estimated audience) for your workspace |
| [`create-campaign-brief`](https://app.pipeline.help/developers/api?operation=create-campaign-brief) | Expand a chosen idea into a full structured campaign brief (ICP rubric, targeting filters, required research signals, message decision tree, frameworks, cadence) |
| [`save-campaign-brief`](https://app.pipeline.help/developers/api?operation=save-campaign-brief) | Validate and persist a campaign brief authored by the caller |
| [`update-campaign-brief`](https://app.pipeline.help/developers/api?operation=update-campaign-brief) | Edit an existing campaign brief without hosted AI |
| [`preview-campaign-revision`](https://app.pipeline.help/developers/api?operation=preview-campaign-revision) | Deterministically preview a prelaunch campaign revision |
| [`apply-campaign-revision`](https://app.pipeline.help/developers/api?operation=apply-campaign-revision) | Apply an exact previewed prelaunch campaign revision after confirmation |
| [`list-gtm-assets`](https://app.pipeline.help/developers/api?operation=list-gtm-assets) | List offering-scoped direct offers, front-end offers, and lead magnets, optionally filtered by lifecycle |
| [`create-gtm-asset-candidate`](https://app.pipeline.help/developers/api?operation=create-gtm-asset-candidate) | Create a caller-authored GTM asset candidate for one core offering |
| [`update-gtm-asset-candidate`](https://app.pipeline.help/developers/api?operation=update-gtm-asset-candidate) | Edit an unapproved GTM asset candidate, or create a superseding version when the selected asset is immutable. |
| [`approve-gtm-asset`](https://app.pipeline.help/developers/api?operation=approve-gtm-asset) | Approve and freeze one reviewed offering-scoped GTM asset version |
| [`retire-gtm-asset`](https://app.pipeline.help/developers/api?operation=retire-gtm-asset) | Retire one GTM asset from new selection while preserving historical bindings |
| [`delete-gtm-asset-draft`](https://app.pipeline.help/developers/api?operation=delete-gtm-asset-draft) | Hard-delete only an unapproved, unbound GTM asset draft |
| [`validate-campaign-brief`](https://app.pipeline.help/developers/api?operation=validate-campaign-brief) | Run the deterministic brief quality gate (the parity enforcer): proof points must trace to real GTM case studies/offers, decision-tree conditions must reference declared signals, the value proposition must link to a distinct ICP pain, and audience size must be sane |
| [`activate-brief`](https://app.pipeline.help/developers/api?operation=activate-brief) | Run the brief: validate it (launch-mode gate), flip it to active, and provision its agent-pipeline enrichment table |

### Campaign Briefs

| Operation | Purpose |
| --- | --- |
| [`list-campaign-briefs`](https://app.pipeline.help/developers/api?operation=list-campaign-briefs) | List campaign briefs in the workspace |
| [`get-campaign-brief`](https://app.pipeline.help/developers/api?operation=get-campaign-brief) | Fetch one campaign brief by id |
| [`run-brief-scorecard`](https://app.pipeline.help/developers/api?operation=run-brief-scorecard) | Compute and return the list-quality scorecard for a brief: overall score, A-F grade, top issues |
| [`get-icp-tuning-sample`](https://app.pipeline.help/developers/api?operation=get-icp-tuning-sample) | Start the ICP Prompt Builder QA loop for a campaign brief |
| [`revise-icp-rubric`](https://app.pipeline.help/developers/api?operation=revise-icp-rubric) | Revise a brief ICP rubric from QA corrections on a canary sample |
| [`save-icp-rubric`](https://app.pipeline.help/developers/api?operation=save-icp-rubric) | Persist a revised ICP rubric onto a campaign brief |
| [`run-icp-canary-gate`](https://app.pipeline.help/developers/api?operation=run-icp-canary-gate) | Run the canary quality gate for a brief after ICP scoring a sample |
| [`list-brief-metrics`](https://app.pipeline.help/developers/api?operation=list-brief-metrics) | Send, reply, and meeting metrics for every brief in the workspace |
| [`provision-brief-table`](https://app.pipeline.help/developers/api?operation=provision-brief-table) | Create or repair the Agent Teams enrichment table for a campaign brief |
| [`preview-campaign-source`](https://app.pipeline.help/developers/api?operation=preview-campaign-source) | Persist the exact campaign-bound sourcing preview before pilot rows are written |
| [`preview-campaign-canary`](https://app.pipeline.help/developers/api?operation=preview-campaign-canary) | Resolve up to 10 campaign-table rows through the approved brief variable plan |

### Workflows v2 (Plays)

| Operation | Purpose |
| --- | --- |
| [`list-plays`](https://app.pipeline.help/developers/api?operation=list-plays) | List every system play available across the platform |
| [`get-play`](https://app.pipeline.help/developers/api?operation=get-play) | Fetch the full definition of a single system play by id |
| [`list-workflows`](https://app.pipeline.help/developers/api?operation=list-workflows) | List all custom GTM workflows in the workspace |
| [`get-workflow`](https://app.pipeline.help/developers/api?operation=get-workflow) | Fetch one workflow by id |
| [`create-workflow`](https://app.pipeline.help/developers/api?operation=create-workflow) | Create a new empty workflow shell in the workspace |
| [`update-workflow`](https://app.pipeline.help/developers/api?operation=update-workflow) | Update an existing workflow |
| [`compile-workflow-from-prompt`](https://app.pipeline.help/developers/api?operation=compile-workflow-from-prompt) | Turn a natural-language description into a runnable workflow plan |
| [`run-workflow`](https://app.pipeline.help/developers/api?operation=run-workflow) | Execute an explicitly identified saved workflow against a batch of input records |
| [`list-workflow-runs`](https://app.pipeline.help/developers/api?operation=list-workflow-runs) | List recent executions of a workflow |
| [`get-workflow-run`](https://app.pipeline.help/developers/api?operation=get-workflow-run) | Fetch the structured execution log for one workflow run |

<!-- TOOL_INDEX_END -->

For review-only influencer QA, call `track-influencer` with `status: "paused"` and `shouldFollow: false`, then `discover-tracked-posts` with an explicit limit (maximum 5). Read the saved post before authoring `save-comment-draft`. These operations do not authorize posting or scheduled polling.
