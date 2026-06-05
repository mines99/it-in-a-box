# IT in a Box

> Open-source enterprise IT stack with an AI agent management layer. Deploy a full IT department's tooling on-demand — self-hosted, cost-effective, and autonomously managed by AI agents.

## Concept

Every tool a company needs from an IT perspective, using open-source equivalents to enterprise commercial products. A single deployable stack with an agentic AI layer on top that monitors, operates, and escalates — reducing the need for a large IT headcount.

## Core Stack

| Category | Tool | Purpose |
|---|---|---|
| **ITSM / Help Desk** | [Zammad](https://zammad.org) | Ticketing, SLA tracking, email/chat/phone channels |
| **CRM** | [Twenty](https://twenty.com) | Customer relationships, pipeline, contact management |
| **Identity / SSO** | [Authentik](https://goauthentik.io) | IAM, SAML/OIDC SSO, MFA, LDAP provider |
| **Monitoring** | [Grafana + Prometheus + Loki](https://grafana.com) | Metrics, logs, alerting, dashboards |
| **Security / SIEM** | [Wazuh](https://wazuh.com) | Endpoint detection, log analysis, threat intelligence |
| **Asset Management** | [Snipe-IT](https://snipeitapp.com) | Hardware/software inventory, CMDB, lifecycle |
| **Project Management** | [Plane](https://plane.so) | Issues, sprints, cycles, roadmaps |
| **Team Communications** | [Mattermost](https://mattermost.com) | Messaging, channels, integrations, self-hosted Slack |
| **Networking / VPN** | [Headscale + WireGuard](https://headscale.net) | Zero-trust mesh networking, remote access |
| **Wiki / Knowledge Base** | [Docmost](https://docmost.com) | Collaborative docs, permissions, version history |
| **Reverse Proxy / TLS** | [Traefik](https://traefik.io) | Auto TLS, routing, middleware, UI management |
| **Notifications** | [Apprise](https://github.com/caronc/apprise) | Unified alerting to Slack, Telegram, email, etc. |
| **Source Control** | [Gitea](https://gitea.io) | Self-hosted Git with CI/CD, code review, packages |
| **Backup** | [Restic + Autorestic](https://restic.net) | Encrypted incremental backups to local or cloud |
| **File Sync** | [Sync-in](https://github.com/Sync-in/server) | Self-hosted cross-device file synchronization server |
| **File Sharing** | [Locker](https://github.com/zmeyer44/Locker) | Dropbox-style file system on own S3/R2/local storage |

## AI Agent Layer

The differentiator. An AI agent mesh sits on top of the entire stack and handles:

- **Auto-triage** — incoming tickets classified, routed, and responded to without human involvement
- **Runbook automation** — agents read monitoring alerts, look up runbooks, and execute remediation
- **Asset lifecycle** — proactive alerts for warranty expiry, license renewal, hardware EOL
- **Onboarding/offboarding** — user provisioned across all systems from a single request
- **Incident response** — SIEM alert → agent investigation → ticket creation → Slack notification → resolution
- **Weekly reporting** — automated digest of ticket volume, system health, security posture

### Agent Tools (from Vault)

| Tool | Role |
|---|---|
| [Hermes Control Interface](https://github.com/xaspx/hermes-control-interface) | Agent management dashboard, cron, token analytics |
| [RunbookHermes](https://github.com/Tommy-yw/RunbookHermes) | Alert → runbook → auto-remediation pipeline |
| [open-multi-agent](https://github.com/JackChen-me/open-multi-agent) | Multi-agent task decomposition and parallelization |
| [Scrumboy](https://github.com/markrai/scrumboy) | AI-integrated kanban/sprint — reads tickets, files bugs |
| [Apprise](https://github.com/caronc/apprise) | Unified notification dispatch from any agent |
| [Homelable](https://github.com/Pouzor/homelable) | Live network topology map, AI-queryable via MCP |
| [pocket-id](https://github.com/pocket-id/pocket-id) | Lightweight OIDC SSO (passkey-only, single container) |
| [agents-observe](https://github.com/simple10/agents-observe) | Real-time agent execution visibility, tool call tracing |
| [Docmost](https://github.com/docmost/docmost) | Collaborative wiki for runbooks, SOPs, IT knowledge base |

### Reference Architecture

| Project | What it demonstrates |
|---|---|
| [Infra AI IT Team Runbook](https://github.com/Mfrostbutter/Infra-AI-IT-Team-Runbook) | 11 specialized agents (8 infra + 3 cyber) running self-hosted stack — tiered haiku/sonnet/opus model routing, append-only change journal, machine-identity secrets |

Key pattern to adopt: **specialist agents (80–150 lines each) dispatched by intent**, not one monolithic agent. Cost math only works at daily use with specialists. Default fleet: 7× haiku · 5× sonnet · opus reserved for multi-domain incidents only.

## Deployment

Target: single-server or small cluster. Docker Compose first, Kubernetes optional.

```
it-in-a-box/
├── stacks/
│   ├── core/          # Traefik, Authentik, monitoring
│   ├── itsm/          # Zammad, Snipe-IT
│   ├── comms/         # Mattermost, Gitea
│   ├── crm/           # Twenty
│   └── agents/        # Hermes, n8n, agent orchestration
├── config/            # Per-stack env templates
├── scripts/           # Bootstrap, backup, health-check
└── docs/              # Architecture, runbooks, onboarding
```

## Selling Point

Most MSPs charge $50-150/user/month for a fragmented stack of commercial tools. IT in a Box delivers the same capability at infra cost + AI labor — approximately 10x cheaper for small/mid businesses, with autonomous management that scales without headcount.

## Status

`[concept]` — architecture phase. Stack selection finalized. Deployment automation and AI agent wiring in progress.

## Related

- [Studio99](https://github.com/mines99/studio99) — AI business automation stack (parent project)
