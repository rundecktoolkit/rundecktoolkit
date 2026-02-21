# Install and Setup

## 1. Build the plugin

```bash
cd plugins/approval-job-step-plugin
./gradlew clean jar
```

Build output:

```text
build/libs/approval-job-step-3.0.8.jar
```

## 2. Install into Rundeck

```bash
cp build/libs/approval-job-step-3.0.8.jar $RDECK_BASE/libext/
```

Restart Rundeck (or reload plugins) after copying.

## 3. Prepare Key Storage

Create SMTP password key in Rundeck Key Storage and copy its path:

- Example path: `keys/mail/smtp-password`
- This value goes into `smtpPasswordPath`

## 4. Configure callback URL and port

Set `approvalUrlBase` to a URL reachable by approvers.

- Local test example: `http://localhost:5556`
- Production example: `https://rundeck-approval.example.com`

The callback server port is parsed from this URL.
Do not reuse a port already occupied by another process.

## 5. Add the workflow step

In the job workflow:

1. Add step: **Approval Job Step**
2. Set required fields:
   - `approvalMessage`
   - `primaryApproverEmail`
   - `smtpServer`
   - `smtpUsername`
   - `smtpPasswordPath`
   - `fromEmailAddress`
3. Save and run the job.

## 6. Optional: seed users for dropdown testing

Approver dropdowns load from Rundeck `rduser` table emails.
Example seed data:

```sql
insert into rduser (login, email, first_name, last_name)
values
('ava.hansen', 'ava.hansen@example.com', 'Ava', 'Hansen'),
('diego.silva', 'diego.silva@example.com', 'Diego', 'Silva'),
('luca.bernard', 'luca.bernard@example.com', 'Luca', 'Bernard'),
('martin.vanson', 'martin.vanson@example.com', 'Martin', 'Vanson'),
('priya.nair', 'priya.nair@example.com', 'Priya', 'Nair');
```

## 7. Verify end to end

1. Trigger job execution.
2. Confirm primary approver receives email.
3. Click approve or deny link.
4. Confirm workflow transitions correctly.
