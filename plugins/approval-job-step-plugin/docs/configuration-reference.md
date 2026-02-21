# Configuration Reference

## Required vs optional fields

| Property | Required | Default | Description |
| --- | --- | --- | --- |
| `approvalMessage` | Yes | n/a | Text sent to approvers. |
| `approvalTimeoutMinutes` | No | `60` | Maximum wait time for approval. |
| `autoApproveOnTimeout` | No | `false` | If true, timeout counts as approved; if false, timeout fails step. |
| `primaryApproverEmail` | Yes | n/a | Primary approver email (dropdown + free input). |
| `secondaryApproverEmail` | No | empty | Optional escalation approver email. |
| `escalationTimeMinutes` | No | `30` | Delay before escalation email is sent. |
| `smtpServer` | Yes | n/a | SMTP host. |
| `smtpPort` | No | `587` | SMTP port. |
| `smtpUsername` | Yes | n/a | SMTP username. |
| `smtpPasswordPath` | Yes | n/a | Rundeck Key Storage path to SMTP password. |
| `fromEmailAddress` | Yes | n/a | Sender email address. |
| `useTls` | No | `true` | Enables STARTTLS for SMTP transport. |
| `approvalUrlBase` | No | `http://localhost:5555` | Base URL for callback links. Port is used for local callback server bind. |
| `checkIntervalSeconds` | No | `30` | Poll interval while step waits for approval callback. |

## Runtime decision logic

| Situation | Outcome |
| --- | --- |
| Primary approver clicks approve | Step returns `approved`; workflow continues. |
| Primary or secondary approver clicks deny | Step returns `denied`; step fails. |
| No response before timeout and `autoApproveOnTimeout=true` | Step returns `approved`; workflow continues. |
| No response before timeout and `autoApproveOnTimeout=false` | Step returns `timeout`; step fails and execution terminates. |
| Secondary approver configured and elapsed time >= `escalationTimeMinutes` | Escalation email sent once to secondary approver. |

## Approver dropdown source

Dropdown values come from Rundeck database users (`rduser.email`).

Lookup behavior:

1. Use env vars when present:
   - `RUNDECK_DATABASE_URL`
   - `RUNDECK_DATABASE_USERNAME`
   - `RUNDECK_DATABASE_PASSWORD`
   - `RUNDECK_DATABASE_DRIVER` (optional)
2. Fallback to `$RDECK_BASE/server/config/rundeck-config.properties`.
3. If no users can be loaded, dropdown can be empty (free input still allowed).

## SMTP password path behavior

- `smtpPasswordPath` must reference an existing key in Rundeck Key Storage.
- The plugin resolves it via storage tree API at execution time.
- Missing key causes configuration failure before email send.

## Recommended baseline config

For initial production rollout:

- `approvalTimeoutMinutes=15`
- `autoApproveOnTimeout=false`
- `escalationTimeMinutes=5`
- `checkIntervalSeconds=15`
- `approvalUrlBase=https://<public-hostname>`

Tune these values based on your thread/worker capacity and approval response SLA.
