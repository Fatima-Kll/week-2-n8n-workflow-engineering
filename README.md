# Form-to-Google Sheets Automation with n8n

An automated service request processing workflow built with **n8n**, **Google Sheets**, and **Gmail**. The workflow collects customer requests through a form, validates submitted information, stores valid submissions in Google Sheets, and sends email notifications.

## Project Overview

This project demonstrates how to design a multi-step business workflow using n8n.

The goal is to automate the initial handling of service requests while separating valid submissions from requests that fail validation.

## Workflow Architecture

```text
                 Form Trigger
                      |
                IF Validation
                 /         \
              TRUE         FALSE
               |             |
       Google Sheets     Edit Fields
       Append Row            |
               |         Gmail Alert
          Gmail Confirmation
```

### Workflow Steps

**1. Form Submission**

The Form Trigger collects:
- Full Name
- Email
- Service
- Message (optional)

**2. Input Validation**

An IF node checks that the required fields are not empty:
- Full Name
- Email
- Service

**3. Valid Submission — TRUE Branch**

- Appends the submitted information to Google Sheets.
- Sends a confirmation email to the customer.

**4. Rejected Submission — FALSE Branch**

- Adds rejection metadata using an Edit Fields node.
- Records the rejection status, reason, and timestamp.
- Sends an internal Gmail notification containing the submission details.

## Technologies and Tools

- **n8n** — Workflow automation and orchestration
- **Google Sheets** — Request storage
- **Gmail** — Email notifications
- **OAuth 2.0** — Google service authentication
- **JSON** — Workflow data structure
- **Expressions** — Dynamic data mapping between nodes

## Concepts Practiced

- Form-based workflow triggers
- Multi-node workflow design
- Conditional logic using IF
- Data mapping and expressions
- Handling JSON objects
- Google Sheets integration
- Gmail integration
- OAuth 2.0 authentication
- Separate processing paths for valid and rejected submissions
- Execution testing and debugging

## Repository Structure

```text
workflow/
    form-to-google-sheets.json

documentation/
    workflow-architecture.md
    test-cases.md
    error-handling.md

screenshots/
    workflow-overview.png
    successful-execution.png
    google-sheets-result.png
    rejection-notification.png
```

## Setup and Configuration

1. Install and run n8n.
2. Import the workflow JSON file.
3. Configure your Google Sheets OAuth2 credentials.
4. Configure your Gmail OAuth2 credentials.
5. Select your own Google spreadsheet and worksheet.
6. Review the node mappings and email settings.
7. Test the workflow using the Form Trigger.

**Note:** Credentials and personal configuration details are not included in this repository. You must configure your own Google accounts and spreadsheet.

## Project Status

The core workflow has been implemented and tested, including:
- Successful form submission and processing.
- Google Sheets data insertion.
- Customer confirmation email.
- Rejection metadata generation.
- Internal rejection notification.

Additional failure scenarios and advanced error-handling improvements are documented separately.

## Learning Outcome

This project strengthened my practical understanding of workflow engineering, data transformation, conditional processing, API integrations, and debugging in n8n.

It is part of my hands-on journey toward building reliable AI and business automation solutions.
