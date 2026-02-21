# Approval Job Step Plugin

Community-maintained Rundeck workflow step plugin for email-based approvals with escalation and callback links.

## Why use this plugin?

- Inserts an explicit approval gate in a workflow.
- Sends email-based `Approve` / `Deny` links to approvers.
- Supports sequential escalation from primary to secondary approver.
- Supports timeout behavior:
  - auto-approve and continue, or
  - fail step and terminate execution.
- Includes a custom green check icon in the workflow step picker.

## Important operational warning

**WARNING: every pending approval keeps execution resources active until approved, denied, or timed out.**

Pending approvals are not "free waits". At scale, many open approvals can reduce worker/thread capacity and slow other jobs.

## Quick start

1. Build:
```bash
./gradlew clean jar
```

2. Copy JAR:
```bash
cp build/libs/approval-job-step-3.0.8.jar $RDECK_BASE/libext/
```

3. Restart Rundeck or reload plugins.
4. Add **Approval Job Step** to a workflow and configure SMTP, approvers, and callback URL.

## Compatibility

- Rundeck 5.x (tested in local rebuild environment)
- Plugin service: `WorkflowStep`
- Plugin ID: `approval-job-step`
- Author: `Rundeck Community`

## Documentation

- [Install and setup guide](./docs/install-and-setup.md)
- [Configuration reference](./docs/configuration-reference.md)
- [Operations and capacity guidance](./docs/operations-and-capacity.md)
- [Troubleshooting](./docs/troubleshooting.md)

## Behavior summary

- Primary approver receives email immediately.
- If no response and secondary approver is configured, escalation email is sent after `escalationTimeMinutes`.
- Step polls for callback until timeout or response.
- Result mapping:
  - `approved` -> workflow continues.
  - `denied` -> step fails.
  - `timeout`:
    - if `autoApproveOnTimeout=true`: continue as approved.
    - if `autoApproveOnTimeout=false`: step fails and job execution terminates.

## Security notes

- SMTP password is read from Rundeck Key Storage (`smtpPasswordPath`), not from plaintext step config.
- Approval callbacks are tokenized (`id` + `token`) and validated server-side.
- Use HTTPS for `approvalUrlBase` in production.
