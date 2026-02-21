# Troubleshooting

## "Failed to start callback server on port ..."

Cause:

- The callback port is already in use.
- Another Rundeck instance/plugin process already bound the same port.

Fix:

1. Change `approvalUrlBase` to an unused port.
2. Restart Rundeck after config changes.
3. Verify bind status:

```bash
lsof -iTCP -sTCP:LISTEN | grep 5555
```

## Approval link opens but execution does not continue

Cause:

- Callback URL is not reachable from approver browser.
- Token mismatch from stale/old link.

Fix:

1. Use fresh email link from latest execution.
2. Confirm URL host/port in `approvalUrlBase` is reachable.
3. Confirm no reverse proxy/firewall block for callback endpoint.

## "Approval message is required" when message is set

Cause:

- Step configuration not saved in the job definition.
- Edited step in UI but saved only workflow draft partially.

Fix:

1. Open the step configuration and re-enter `approvalMessage`.
2. Save step and save job.
3. Re-run execution.

## SMTP password path stays empty after key picker selection

Cause:

- Key path not under accessible storage root.
- Key not present or ACL denies access.

Fix:

1. Ensure key exists under `keys/...`.
2. Confirm ACL policy allows storage read for the executing context.
3. Paste key path manually to verify behavior.

## No users in approver dropdown

Cause:

- No `rduser` emails available.
- DB connection env/config missing.

Fix:

1. Verify `RUNDECK_DATABASE_URL` (or rundeck-config dataSource values).
2. Confirm `rduser` table has non-empty `email`.
3. Check logs for:
   - `ApprovalJobStep: loaded X users for dropdowns`
   - DB connection warnings/errors.

## Job times out unexpectedly

Cause:

- `approvalTimeoutMinutes` too low.
- Email delivery or response delays.

Fix:

1. Increase timeout value.
2. Configure secondary approver escalation.
3. Reduce `checkIntervalSeconds` for faster callback pickup.
