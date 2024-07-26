# Project: Soccer Email Automation

## Overview
This project involves setting up automated daily sign-up emails for a soccer group, dynamically managing a distribution list, generating motivational content, and counting participant responses. The system also includes handling admin commands to add or remove email addresses from the distribution list and sending assistance emails for unrecognized commands.

## Notes

### Note 1: Initial Setup and Daily Sign-Up Email

#### Summary
- **Objective**: Send a daily sign-up email with dynamic content and count participant responses.
- **Components**:
  - Daily email trigger
  - Dynamic content generation using OpenAI API
  - Variable initialization for email components

#### Steps
1. **Initialize Variables**:
    - `GameCancelled`: Boolean
    - `SignUpCount`: Integer
    - `SpecialMessage`: String
    - `DynamicMessage`: String
    - `WeatherMessage`: String
    - `OpeningLine`: String
    - `Location`: String (`Bowman Field`)
    - `GameTime`: String (`1300 - 1400`)

2. **Generate Dynamic Content Using OpenAI**:
    - HTTP action to call OpenAI API
    - Parse JSON action to extract response
    - Set variable for `DynamicMessage`

3. **Send Daily Sign-Up Email**:
    - Send an email with dynamic content including date, time, location, and motivational message.

4. **Count Participants**:
    - Trigger when a new email arrives
    - Extract email content
    - Check for sign-up format
    - Increment `SignUpCount` variable

#### Example Daily Sign-Up Email
```plaintext
@{variables('DynamicMessage')}

@{variables('WeatherMessage')}

Hello,

Reply to this email with your sign-up in the format 'number) name'. Example: '3) Jamie'

Game details:
Date: @{outputs('FormattedDate')}
Time: @{variables('GameTime')}
Location: @{variables('Location')}

Special Message: @{variables('SpecialMessage')}
####
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
<details>
  <summary><h2> Managing Distribution List</h2> </summary>
  


#### Summary
- **Objective**: Dynamically manage the distribution list via email commands.
- **Components**:
  - Handling admin commands to add or remove emails
  - Sending assistance emails for unrecognized commands

#### Steps
1. **Add Email Address**:
    - Condition to check if the email subject starts with `ADD:`
    - Extract email address
    - Add the email address to the Excel sheet
    - Send confirmation email to the sender

2. **Remove Email Address**:
    - Condition to check if the email subject starts with `REMOVE:`
    - Extract email address
    - List rows in the Excel sheet
    - Delete the row where the email matches
    - Send confirmation email to the sender

3. **Assistance Email**:
    - Default case for unrecognized commands
    - Send a troubleshooting email with instructions

#### Example Email Commands
- **Add Email Command**:
  - Subject: `ADD:email1@example.com`
  - Body: `Please add this email to the distribution list.`

- **Remove Email Command**:
  - Subject: `REMOVE:email1@example.com`
  - Body: `Please remove this email from the distribution list.`

#### Example Assistance Email
```plaintext
We could not process your request. Please ensure you are using the correct format for adding or removing emails:

- To add an email, use the subject: ADD:email@example.com
- To remove an email, use the subject: REMOVE:email@example.com

Please resend your email with the correct format.
```  
</details>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary><h2>OpenAI API Integration</h2> </summary>
#### Summary
**Objective**: Integrate OpenAI API to generate dynamic motivational messages.

**Components**:
- HTTP action to call OpenAI API
- Parse JSON action to extract response
- Set variable for `DynamicMessage`

#### Steps

**HTTP Action**:
- Method: POST
- URI: `https://api.openai.com/v1/engines/davinci-codex/completions`
- Headers:
  - Authorization: Bearer YOUR_API_KEY
  - Content-Type: application/json
- Body:
  ```json
  {
    "prompt": "Generate a motivational message for a soccer game. Make it engaging and friendly.",
    "max_tokens": 50
  }


**HTTP Action**:
- Extract the Response
```
  {
  "type": "object",
  "properties": {
    "choices": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "text": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

</details>
