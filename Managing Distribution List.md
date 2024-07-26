
### Note 2: Managing Distribution List

#### Summary
**Objective**: Dynamically manage the distribution list via email commands.

**Components**:
- Handling admin commands to add or remove emails
- Sending assistance emails for unrecognized commands

#### Steps

**Add Email Address**:
- Condition to check if the email subject starts with `ADD:`
- Extract email address
- Add the email address to the Excel sheet
- Send confirmation email to the sender

**Remove Email Address**:
- Condition to check if the email subject starts with `REMOVE:`
- Extract email address
- List rows in the Excel sheet
- Delete the row where the email matches
- Send confirmation email to the sender

**Assistance Email**:
- Default case for unrecognized commands
- Send a troubleshooting email with instructions

#### Example Email Commands

**Add Email Command**:
- Subject: `ADD:email1@example.com`
- Body: `Please add this email to the distribution list.`

**Remove Email Command**:
- Subject: `REMOVE:email1@example.com`
- Body: `Please remove this email from the distribution list.`

#### Example Assistance Email
```plaintext
We could not process your request. Please ensure you are using the correct format for adding or removing emails:

- To add an email, use the subject: ADD:email@example.com
- To remove an email, use the subject: REMOVE:email@example.com

Please resend your email with the correct format.
