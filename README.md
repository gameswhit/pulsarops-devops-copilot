# PulsarOps — AI DevOps Copilot

PulsarOps is an AI-native DevOps copilot that monitors, detects, and self-heals your infrastructure in real-time. Built on **MiMo-Series**, **Claude-Series**, and **DeepSeek-Series** models.

## Features
- **Live Telemetry Ingest** — metrics, logs, and traces from Prometheus, Datadog, Grafana, CloudWatch, and OpenTelemetry.
- **Anomaly Detection** — MiMo-powered unsupervised models spot drift, saturation, and latency spikes 5 minutes before they become incidents.
- **Auto-Remediation** — scale pods, roll back deploys, toggle feature flags, flush caches — with Terraform/Pulumi diffs.
- **Incident Timeline** — auto-generated incident reports with root-cause analysis, owner, blast radius, and post-mortem draft.
- **Canary Deployments** — progressive rollouts with automatic rollback on error-rate increase.
- **SLO Tracking** — define SLIs, track error budgets, and get proactive alerts.
- **Multi-Cloud Aware** — one pane for AWS, GCP, Azure, and bare-metal.
- **ChatOps Native** — interact from Slack, Teams, or Discord with natural-language queries.

## Quickstart
```bash
helm repo add pulsarops https://charts.pulsarops.dev
helm install pulsarops pulsarops/pulsarops-agent \
    --set apiKey=$PULSAR_API_KEY \
    --set model=mimo-v2.5-pro
pulsarctl status
```

## Ask your infrastructure
```bash
pulsarctl ask "why is api-gateway slow?"
# → Root cause: billing-svc connection pool exhausted (200/200 used)
# → Suggested fix: increase pool to 400 or revert to v2.13.2
# → Action: PR #1847 opened (revert to v2.13.2)
pulsarctl approve 1847
# ✓ Rolled out · latency back to 141ms · 3m 12s
```

## Architecture
```
┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│  Telemetry   │ → │   Anomaly    │ → │  Remediation │
│   Ingest     │   │  Classifier  │   │    Agent     │
│ Prometheus   │   │  (MiMo Pro)  │   │ (Terraform)  │
└──────────────┘   └──────────────┘   └──────────────┘
                                              │
                              ┌────────────────┴───────────┐
                              │  Apply Diff · Verify SLO   │
                              │  Report · Close Incident   │
                              └────────────────────────────┘
```

## Sister Project
PulsarOps handles operations (running code in production). **NebulaCraft AI Studio** handles code synthesis (writing the code). Together they form a full AI-native dev-to-ops loop.
→ [NebulaCraft AI Studio](https://nebulacraft-ai-studio.vercel.app)

## Status
- v2.3 in production
- 3,200+ clusters monitored
- 4.7M metrics analyzed / day
- 92% incidents auto-resolved

## License
Helm chart, agent, anomaly models — MIT.

---

Built with PulsarOps. Powered by MiMo. Part of the **100T Token Initiative**.
