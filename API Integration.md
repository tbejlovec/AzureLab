### Note 3: OpenAI API Integration

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


**Parse Action**
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

