<p align="center">
  <img src="https://img.shields.io/badge/Rundeck-Toolkit-2C6FBB?style=for-the-badge&logoColor=white" alt="Rundeck Toolkit"/>
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge" alt="Status"/>
  <img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="License"/>
</p>

<h1 align="center">Rundeck Toolkit</h1>

<p align="center">
  <strong>Community plugins, example jobs, and automation patterns for Rundeck &amp; PagerDuty Runbook Automation</strong>
</p>

<p align="center">
  <em>Built by practitioners. Battle-tested in production. Shared freely.</em>
</p>

---

> **Disclaimer:** This repository is an independent community project. It is **not officially supported, endorsed, or maintained** by PagerDuty, Inc. or Rundeck, Inc. All content is provided **as-is** under the MIT license with no warranty or guarantee of support. Use at your own discretion.

---

## What Is This?

Rundeck Toolkit is a curated collection of plugins, job definitions, workflow patterns, and integration examples built from real-world enterprise automation work. Every piece of content here has been developed to solve actual problems encountered during Rundeck and Runbook Automation deployments.

Whether you're just getting started with Rundeck or you're scaling automation across hundreds of nodes, there's something here for you.

---

## Available Plugins

### AI & LLM Integrations

| Plugin | Description | Version | Links |
|--------|-------------|---------|-------|
| **[Anthropic Query](https://github.com/rundecktoolkit/plugin-workflow-anthropic)** | Integrate Claude AI models into workflow steps | v2.0.0 | [Releases](https://github.com/rundecktoolkit/plugin-workflow-anthropic/releases) |
| **[OpenAI Chat](https://github.com/rundecktoolkit/plugin-workflow-openai)** | Integrate GPT models into workflow steps | v1.0.0 | [Releases](https://github.com/rundecktoolkit/plugin-workflow-openai/releases) |
| **[Ollama Query](https://github.com/rundecktoolkit/plugin-workflow-ollama)** | Query locally-hosted Ollama models | v2.0.0 | [Releases](https://github.com/rundecktoolkit/plugin-workflow-ollama/releases) |

### Plugin Compatibility

| Platform | Supported Versions |
|----------|-------------------|
| Rundeck Community | 4.x, 5.x |
| Runbook Automation (Self-Hosted) | 4.x, 5.x |

### Prerequisites

All AI plugins require the **[JQ JSON Log Filter](https://github.com/rundeck-plugins/jq-json-logfilter)** plugin to process JSON output.

---

## Quick Start

### Install a Plugin via UI (Recommended)

1. Download the JAR from the plugin's [Releases](https://github.com/rundecktoolkit) page
2. In Rundeck, navigate to **System Menu → Plugins → Upload Plugin**
3. Select the downloaded JAR file
4. The plugin is immediately available—no restart required

### Import an Example Job

Each plugin includes ready-to-use example jobs in its `examples/` folder.

```bash
# Using the Rundeck CLI
rd jobs load --file examples/Anthropic_Example.json \
  --project MyProject --format json

# Using the API
curl -X POST "https://your-rundeck:4440/api/44/project/MyProject/jobs/import" \
  -H "X-Rundeck-Auth-Token: $RD_TOKEN" \
  -H "Content-Type: application/json" \
  --data-binary @examples/Anthropic_Example.json
```

---

## Repository Naming Convention

All plugins follow this naming pattern:

```
plugin-{type}-{name}
```

| Component | Description | Examples |
|-----------|-------------|----------|
| `plugin` | Required prefix | — |
| `{type}` | Plugin type | `workflow`, `notification`, `node`, `storage` |
| `{name}` | Plugin name | `anthropic`, `openai`, `ollama` |

---

## Contributing

Contributions are welcome and encouraged. If you've built something useful with Rundeck, this is a good home for it.

### Submission Requirements

Every plugin submission must include:

| Requirement | Description |
|-------------|-------------|
| **Repository naming** | Follow `plugin-{type}-{name}` convention |
| **README.md** | Documentation following the standard template |
| **LICENSE** | MIT license with `Copyright (c) rundecktoolkit` |
| **Example job** | At least one importable job in `examples/` folder |
| **Release** | JAR file with proper release notes |

### README Requirements

- Rundeck Community and Runbook Automation badges
- Compatibility table (minimum Rundeck 4.x)
- Prerequisites section (including JQ JSON Log Filter if applicable)
- UI installation as primary method
- Log filter setup instructions (if plugin outputs JSON)
- Link to example job(s)
- Disclaimer and support information

### Example Job Requirements

- Complete, importable Rundeck job definition
- Demonstrates primary plugin functionality
- Includes log filter configuration if plugin outputs JSON
- Uses placeholder paths for keys (e.g., `keys/project/{plugin}/api_key`)

### How to Submit

1. Fork the relevant repository or create a new one following naming conventions
2. Ensure all requirements are met
3. Submit a pull request or request to join the organization
4. Include a description of what the plugin does and why it's useful

---

## Build Configuration Standards

### build.gradle

```groovy
jar {
    manifest {
        attributes 'Rundeck-Plugin-Author': 'rundecktoolkit'
        attributes 'Rundeck-Plugin-Rundeck-Compatibility-Version': '4.x'
        attributes 'Rundeck-Plugin-License': 'MIT'
        attributes 'Rundeck-Plugin-Source-Link': 'https://github.com/rundecktoolkit/{repo-name}'
    }
}
```

### Release Notes Must Include

- Feature summary
- Prerequisites (especially JQ JSON Log Filter)
- Compatibility table
- Installation instructions (UI method)
- Basic usage steps including log filter setup
- Link to README
- Disclaimer

---

## Related Resources

| Resource | Link |
|----------|------|
| Rundeck Documentation | [docs.rundeck.com](https://docs.rundeck.com) |
| PagerDuty Automation | [pagerduty.com/platform/automation](https://www.pagerduty.com/platform/automation/) |
| Rundeck Plugin Development | [docs.rundeck.com/docs/developer](https://docs.rundeck.com/docs/developer/) |
| JQ JSON Log Filter | [github.com/rundeck-plugins/jq-json-logfilter](https://github.com/rundeck-plugins/jq-json-logfilter) |
| Community Forums | [community.pagerduty.com](https://community.pagerduty.com/) |

---

## Project Stats

![GitHub stars](https://img.shields.io/github/stars/rundecktoolkit?style=social)
![Last commit](https://img.shields.io/github/last-commit/rundecktoolkit/plugin-workflow-anthropic)

---

<p align="center">
  <sub>Not affiliated with or supported by PagerDuty, Inc. or Rundeck, Inc.</sub>
</p>
