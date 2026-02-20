<p align="center">
  <img src="https://img.shields.io/badge/Rundeck-Toolkit-2C6FBB?style=for-the-badge&logoColor=white" alt="Rundeck Toolkit"/>
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge" alt="Status"/>
  <img src="https://img.shields.io/badge/License-Apache_2.0-blue?style=for-the-badge" alt="License"/>
</p>

<h1 align="center">🔧 Rundeck Toolkit</h1>

<p align="center">
  <strong>Community plugins, example jobs, and automation patterns for Rundeck &amp; PagerDuty Runbook Automation</strong>
</p>

<p align="center">
  <em>Built by practitioners. Battle-tested in production. Shared freely.</em>
</p>

---

> **⚠️ Disclaimer:** This repository is an independent community project. It is **not officially supported, endorsed, or maintained** by PagerDuty, Inc. or Rundeck, Inc. All content is provided **as-is** under the Apache 2.0 license with no warranty or guarantee of support. Use at your own discretion.

---

## What Is This?

Rundeck Toolkit is a curated collection of plugins, job definitions, workflow patterns, and integration examples built from real-world enterprise automation work. Every piece of content here has been developed to solve actual problems encountered during Rundeck and Runbook Automation deployments.

Whether you're just getting started with Rundeck or you're scaling automation across hundreds of nodes, there's something here for you.

---

## 📦 Repository Structure

```text
rundecktoolkit/
├── plugins/              # Custom Rundeck plugins (node executors, notification, workflow steps)
├── jobs/                 # Exportable job definitions (.yaml/.xml)
│   ├── infrastructure/   # Server, VM, and cloud management
│   ├── incident/         # Incident response and remediation
│   ├── security/         # Compliance checks and patching
│   ├── monitoring/       # Health checks and diagnostics
│   └── maintenance/      # Routine operational tasks
├── patterns/             # Reusable automation design patterns
├── integrations/         # Examples connecting Rundeck to external systems
├── acl-templates/        # Access control policy templates
└── docs/                 # Guides, best practices, and walkthroughs
```

---

## 🚀 Highlights

### Plugins

| Plugin | Description | Type |
| --- | --- | --- |
| **AI Job Documenter** | Auto-generates markdown documentation for job definitions using LLMs | Workflow Step |
| **Dynamic Options Server** | Converts CSV-based lists to JSON API endpoints for Rundeck option providers | Utility |
| **FileWatcher** | Cross-platform file system monitor that triggers Rundeck jobs via webhooks | Event Source |


### Example Job Categories

| Category | What's Included |
| --- | --- |
| **Infrastructure** | VM lifecycle management, disk cleanup, certificate rotation, resource scaling |
| **Incident Response** | Automated diagnostics, log collection, service restarts, runbook execution |
| **Security & Compliance** | CVE scanning, patch management, firewall rule audits, key rotation |
| **Monitoring** | Synthetic health checks, endpoint validation, SLA reporting |
| **Maintenance** | Database housekeeping, log rotation, backup verification, cache clearing |

### Automation Patterns



---

## 🔌 Integration Examples


---

## ⚡ Quick Start

### Import a job definition

```bash
# Using the Rundeck CLI
rd jobs load --file jobs/infrastructure/disk-cleanup.yaml \
  --project MyProject --format yaml
```

```bash
# Using the API
curl -X POST "https://your-rundeck:4440/api/44/project/MyProject/jobs/import" \
  -H "X-Rundeck-Auth-Token: $RD_TOKEN" \
  -H "Content-Type: application/yaml" \
  --data-binary @jobs/infrastructure/disk-cleanup.yaml
```

### Install a plugin

```bash
# Copy plugin to Rundeck's libext directory
cp plugins/my-plugin.jar $RDECK_BASE/libext/

# Or for script-based plugins
cp -r plugins/my-script-plugin $RDECK_BASE/libext/
```

---

## 🤝 Contributing

Contributions are welcome and encouraged. If you've built something useful with Rundeck, this is a good home for it.

### How to contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-automation`)
3. Include a README with your contribution explaining what it does and how to use it
4. Submit a pull request

### Guidelines

- Job definitions should use YAML format where possible
- Remove any environment-specific values (API keys, hostnames, internal URLs)
- Include sample option values or defaults so jobs can be tested without modification
- Document any external dependencies (plugins, scripts, API access)

---

## 📖 Related Resources

| Resource | Link |
| --- | --- |
| Rundeck Documentation | [docs.rundeck.com](https://docs.rundeck.com) |
| PagerDuty Automation | [pagerduty.com/platform/automation](https://www.pagerduty.com/platform/automation/) |
| Rundeck Plugin Development | [docs.rundeck.com/docs/developer](https://docs.rundeck.com/docs/developer/) |
| Community Forums | [community.pagerduty.com](https://community.pagerduty.com/) |

---

## 📊 Project Stats

![GitHub stars](https://img.shields.io/github/stars/rundecktoolkit/rundecktoolkit?style=social)
![GitHub forks](https://img.shields.io/github/forks/rundecktoolkit/rundecktoolkit?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/rundecktoolkit/rundecktoolkit?style=social)
![Last commit](https://img.shields.io/github/last-commit/rundecktoolkit/rundecktoolkit)

---

<p align="center">

</p>

<p align="center">
  <sub>Not affiliated with or supported by PagerDuty, Inc. or Rundeck, Inc.</sub>
</p>
