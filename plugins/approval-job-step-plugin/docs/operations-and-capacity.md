# Operations and Capacity Guidance

## Critical behavior

Each pending approval keeps an execution active while waiting.
This consumes worker/thread capacity until one of these events occurs:

- Approver clicks approve.
- Approver clicks deny.
- Timeout is reached.

## Why this matters

If many jobs wait on approval at once, you can hit execution limits and thread starvation.
Symptoms include:

- Slow job starts.
- Queued executions growing.
- Other workflows delayed behind pending approvals.

## Capacity planning recommendations

1. Keep approval timeout short and explicit.
2. Use escalation to reduce long waits.
3. Set conservative concurrency for jobs that include approval step.
4. Separate high-volume automation from approval-heavy workflows.
5. Monitor pending approval count as an operational metric.

## Suggested guardrails

- Set `approvalTimeoutMinutes` to business-appropriate minimum.
- Prefer `autoApproveOnTimeout=false` unless policy explicitly allows auto-approval.
- Apply project/job-level concurrency controls in Rundeck.
- Document ownership for pending approvals and escalation responders.

## Monitoring checklist

- Track job executions waiting in approval state.
- Track average approval latency.
- Alert on backlog threshold (example: more than 10 pending approvals for 10+ minutes).
- Review SMTP delivery failures, because undelivered mail can hold executions open until timeout.

## Runbook snippet for responders

1. Confirm callback URL is reachable by approvers.
2. Confirm SMTP credentials/key path still valid.
3. Review active pending approvals and cancel stale executions if needed.
4. Adjust timeout/escalation values if backlog repeats.
