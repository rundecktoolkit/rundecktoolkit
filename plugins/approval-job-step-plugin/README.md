# Approval Job Step Plugin

Community-maintained Rundeck workflow step plugin for email-based approvals.

## Key Behavior

- Sends approval links by email (`approve` / `deny`).
- Supports optional escalation to a secondary approver.
- Supports timeout with either:
  - auto-approve, or
  - fail step (terminate job execution).

## Important Operational Warning

`WARNING`: every pending approval keeps execution resources active until it is approved, denied, or timed out.

This means large numbers of pending approvals can exhaust available worker threads/execution capacity.
Design timeout values and concurrency limits accordingly.

## Build

```bash
./gradlew clean jar
```

Build output:

```text
build/libs/approval-job-step-3.0.8.jar
```

## Install

Copy the JAR to your Rundeck `libext` directory and restart/reload plugins.

## Plugin Metadata

- Name: `Approval Job Step`
- Author: `Rundeck Community`
- Service: `WorkflowStep`
- Plugin ID: `approval-job-step`

## Notes

- The callback server binds to the port parsed from `approvalUrlBase`.
- Use a free local port for callback links to avoid conflicts.
- Includes a custom green check icon for workflow step picker visibility.
