# Client Onboarding & Automated Follow-up System

An automated client onboarding and follow-up solution built using **n8n, Tally, Google Sheets, and Gmail**.

The workflow captures new leads, standardizes their information, sends personalized HTML welcome emails, and automatically follows up with clients after three days.

## Overview

The project consists of two automated processes within a single n8n workflow.

### 1. Client Onboarding

When a user submits the Tally form:

1. **Tally Trigger** receives the new submission.
2. **Edit Fields** formats the client's name and removes the leading `+` from the phone number.
3. **Google Sheets** stores the client's information.
4. **Gmail** sends a personalized HTML welcome email.
5. **Google Sheets Update Row** marks the welcome email as sent and calculates the follow-up date.

### 2. Automated Follow-up

A scheduled workflow runs daily at 10:00 AM (Africa/Cairo).

1. **Schedule Trigger** starts the process.
2. **Google Sheets** retrieves records with a follow-up date matching the current date.
3. **IF Node** checks whether the follow-up email has already been sent.
4. **Gmail** sends a personalized HTML follow-up email to eligible clients.
5. **Google Sheets Update Row** marks the follow-up as sent to prevent duplicate emails.

## Technologies Used

| Technology | Purpose |
|---|---|
| n8n | Workflow automation |
| Tally | Client registration form |
| Google Sheets | Client database and tracking |
| Gmail | Personalized HTML email delivery |
| JavaScript Expressions | Data formatting, date calculations, and conditions |

## Google Sheets Structure

| Name | Email | Phone | Welcome Email | Follow-up Date | Follow-up Sent |
|---|---|---|---|---|---|
| Sara Ahmed | sara@example.com | 201000000000 | 1 | 2026-11-20 | 0 |

**Tracking fields:**

- `Welcome Email = 1`: Welcome email successfully sent.
- `Follow-up Date`: Scheduled date, three days after registration.
- `Follow-up Sent = 1`: Follow-up email sent.
- An empty or `0` follow-up status indicates that the follow-up is pending.

## Workflow Features

- Automated lead capture
- Name capitalization and phone number formatting
- Personalized HTML email templates
- Dynamic follow-up date calculation
- Daily scheduled execution
- Conditional email sending
- Follow-up status tracking in Google Sheets

## How to Use

1. Download `n8n_client_onboarding_followup.json`.
2. Import the file into n8n.
3. Configure your Tally, Google Sheets, and Gmail credentials.
4. Select your Tally form and Google Sheets document.
5. Ensure the sheet contains the required column headers.
6. Configure the workflow timezone to `Africa/Cairo` or your preferred timezone.
7. Test both workflow branches before publishing.
8. Publish the workflow to enable automatic execution.

**Note:** The repository contains a sanitized workflow template. Connection details must be configured after importing. Email-based row matching assumes unique email addresses.

## Learning Outcomes

This project helped me gain hands-on experience with event-driven automation, scheduled workflows, data transformation, Google Sheets integration, HTML email generation, and conditional execution using n8n.

## Project Status

Developed and tested as a hands-on automation project. The shared workflow requires configuration and testing in the destination environment.
