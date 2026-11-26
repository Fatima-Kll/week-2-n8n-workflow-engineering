# Workflow Architecture

## Objective

Automate the processing of incoming service requests using n8n, Google Sheets, and Gmail.

## Input

The Form Trigger collects the following fields:

| Field | Type | Required |
|---|---|---|
| Full Name | Text | Yes |
| Email | Email | Yes |
| Service | Dropdown | Yes |
| Message | Textarea | No |

## Processing Logic

### Step 1 — Form Trigger

Starts the workflow when a user submits the service request form.

### Step 2 — IF Validation

Checks whether the following fields are not empty:
- Full Name
- Email
- Service

The node routes each item to one of two branches.

### Step 3 — TRUE Branch

**Google Sheets — Append Row**

Stores the request in the configured spreadsheet.

Stored fields:
- Full Name
- Email
- Service
- Message
- Submission Date

**Gmail — Customer Confirmation**

Sends a confirmation email to the address submitted in the form.

### Step 4 — FALSE Branch

**Edit Fields**

Adds the following metadata:

| Field | Value |
|---|---|
| status | rejected |
| reason | Missing or invalid required information |
| timestamp | Current execution timestamp |

The original form fields are preserved.

**Gmail — Internal Alert**

Sends an email notification to the workflow administrator containing the submission details and rejection metadata.

## Data Flow

```text
Form Data
   |
   v
IF Validation
   |
   +---- TRUE ----> Google Sheets
   |                    |
   |                    v
   |              Customer Email
   |
   +---- FALSE ---> Rejection Metadata
                        |
                        v
                  Internal Alert
```

## External Integrations

- Google Sheets: stores valid service requests.
- Gmail: sends customer confirmations and internal rejection alerts.
- OAuth 2.0: authorizes access to Google services.
