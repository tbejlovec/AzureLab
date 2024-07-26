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
