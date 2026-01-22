---
name: chatgpt-app-builder
description: Build custom ChatGPT apps and GPTs with actions, function calling, and best practices. Use when creating ChatGPT apps, defining GPT actions, building custom GPTs, integrating APIs with ChatGPT, or when user mentions ChatGPT development, GPT actions, or custom GPTs.
---

# ChatGPT App Builder

Build production-ready ChatGPT apps and custom GPTs with actions, proper schema definitions, and best practices for user experience.

## Quick Start

**Creating a Custom GPT:**

1. Go to [ChatGPT](https://chat.openai.com)
2. Navigate to "Explore GPTs" → "Create"
3. Use the GPT Builder or Configure tab
4. Define your GPT's behavior and capabilities

**Adding Actions:**

1. In Configure tab, scroll to "Actions"
2. Click "Create new action"
3. Import OpenAPI schema or define manually
4. Test your action
5. Configure authentication if needed

## GPT Configuration Best Practices

### Name and Description

**Name:**
- Clear, descriptive, 3-5 words max
- Reflects primary function
- Easy to remember

**Description:**
- Concise explanation of what GPT does
- Target audience and use cases
- 1-2 sentences

**Example:**
```
Name: API Documentation Helper
Description: Helps developers create and format API documentation with best practices for REST, GraphQL, and webhook APIs.
```

### Instructions

Write clear, detailed instructions for your GPT's behavior:

```markdown
# Role
You are an expert [role description].

# Capabilities
- Capability 1
- Capability 2
- Capability 3

# Constraints
- Don't do X
- Always verify Y
- When Z happens, do this

# Style
- Be [adjective]
- Use [tone]
- Format responses as [format]

# Examples
[Provide 2-3 concrete examples of good interactions]
```

**Best Practices:**
- ✅ Be specific and detailed
- ✅ Include examples of good responses
- ✅ Define constraints clearly
- ✅ Specify output format preferences
- ✅ Include edge case handling
- ❌ Don't be vague ("be helpful")
- ❌ Don't over-constrain creativity

### Conversation Starters

Provide 4 example prompts that showcase your GPT's capabilities:

```
1. "Create an API endpoint for user authentication"
2. "Review this API response schema for best practices"
3. "Generate OpenAPI spec for a REST API"
4. "Help me debug this webhook integration"
```

**Tips:**
- Show diverse capabilities
- Use real-world scenarios
- Keep them concise and clear
- Make them copy-paste ready

### Knowledge Files

Upload files for your GPT to reference:

**Good use cases:**
- Product documentation
- API specifications
- Style guides
- Data schemas
- Example code
- Reference materials

**Best practices:**
- ✅ Use markdown, text, or PDF formats
- ✅ Keep files under 512MB total
- ✅ Structure content clearly
- ✅ Include table of contents for long docs
- ✅ Use consistent formatting
- ❌ Don't upload binary formats unnecessarily
- ❌ Don't include sensitive data

## Actions and Function Calling

### OpenAPI Schema Structure

Actions require OpenAPI 3.0+ schema:

```yaml
openapi: 3.0.0
info:
  title: My API
  version: 1.0.0
  description: API for my custom GPT
servers:
  - url: https://api.example.com
paths:
  /search:
    get:
      operationId: searchItems
      summary: Search for items
      description: Detailed description of what this endpoint does
      parameters:
        - name: query
          in: query
          required: true
          description: Search query string
          schema:
            type: string
        - name: limit
          in: query
          required: false
          description: Maximum number of results
          schema:
            type: integer
            default: 10
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: object
                properties:
                  results:
                    type: array
                    items:
                      type: object
                      properties:
                        id:
                          type: string
                        title:
                          type: string
                        description:
                          type: string
```

**Key Elements:**
- `operationId`: Unique identifier (ChatGPT uses this)
- `summary`: Brief description shown to users
- `description`: Detailed explanation for the model
- `parameters`: Input parameters with types and descriptions
- `responses`: Expected response structure

### JSON Schema for Actions

When defining actions directly in ChatGPT UI:

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Weather API",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "https://api.weather.com"
    }
  ],
  "paths": {
    "/current": {
      "get": {
        "operationId": "getCurrentWeather",
        "summary": "Get current weather",
        "description": "Returns current weather conditions for a location",
        "parameters": [
          {
            "name": "location",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "City name or coordinates"
          }
        ],
        "responses": {
          "200": {
            "description": "Weather data",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "temperature": {
                      "type": "number"
                    },
                    "conditions": {
                      "type": "string"
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

### Action Best Practices

**Schema Design:**
- ✅ Clear, descriptive operation IDs
- ✅ Detailed parameter descriptions
- ✅ Include examples in descriptions
- ✅ Specify required vs optional parameters
- ✅ Use appropriate data types
- ✅ Document error responses

**API Design:**
- ✅ RESTful conventions
- ✅ Consistent naming
- ✅ Proper HTTP methods (GET, POST, PUT, DELETE)
- ✅ Pagination for list endpoints
- ✅ Rate limiting awareness
- ✅ Meaningful error messages

**Testing:**
- ✅ Test each action individually
- ✅ Test with various input types
- ✅ Test error scenarios
- ✅ Verify response format
- ✅ Check authentication flow

## Authentication

### Authentication Types

**1. API Key (Header)**
```json
{
  "type": "api_key",
  "api_key": {
    "type": "bearer"
  }
}
```

**2. OAuth**
```json
{
  "type": "oauth",
  "oauth": {
    "client_id": "your-client-id",
    "authorization_url": "https://auth.example.com/oauth/authorize",
    "token_url": "https://auth.example.com/oauth/token",
    "scope": "read write"
  }
}
```

**3. Custom (HTTP)**
```json
{
  "type": "custom",
  "custom": {
    "headers": {
      "X-API-Key": "{{API_KEY}}"
    }
  }
}
```

### Security Best Practices

- ✅ Use HTTPS endpoints only
- ✅ Store credentials securely
- ✅ Implement proper OAuth flows
- ✅ Use short-lived tokens when possible
- ✅ Rotate API keys regularly
- ✅ Validate all inputs on server side
- ❌ Don't expose API keys in schema
- ❌ Don't include secrets in knowledge files
- ❌ Don't bypass authentication checks

## Response Formatting

### Structured Responses

ChatGPT handles various response formats:

**JSON (Recommended):**
```json
{
  "status": "success",
  "data": {
    "items": [...],
    "total": 42
  },
  "metadata": {
    "page": 1,
    "per_page": 10
  }
}
```

**Plain Text:**
```
Result: Success
Details: Operation completed
Items found: 42
```

**Markdown:**
```markdown
# Results

Found **42 items**:
- Item 1
- Item 2
- Item 3
```

### Error Handling

Provide helpful error messages:

```json
{
  "error": {
    "code": "INVALID_INPUT",
    "message": "The 'email' parameter must be a valid email address",
    "details": {
      "field": "email",
      "provided": "invalid-email"
    }
  }
}
```

**Error Response Best Practices:**
- ✅ Clear error messages
- ✅ Actionable guidance
- ✅ Specific error codes
- ✅ Context about what went wrong
- ✅ Suggestions for fixing

## Testing Your GPT

### Manual Testing Checklist

**Functionality:**
- [ ] All actions work as expected
- [ ] Error cases are handled gracefully
- [ ] Authentication works correctly
- [ ] Response format is consistent
- [ ] Edge cases are handled

**User Experience:**
- [ ] Instructions are clear
- [ ] Conversation starters work
- [ ] Responses are helpful
- [ ] Tone is appropriate
- [ ] Knowledge files are referenced correctly

**Performance:**
- [ ] Actions respond quickly (< 5s)
- [ ] No rate limiting issues
- [ ] Large responses are handled
- [ ] Timeouts are managed

### Test Scenarios

Create test cases for common scenarios:

1. **Happy path**: Normal, expected usage
2. **Missing parameters**: Required fields not provided
3. **Invalid input**: Wrong data types or formats
4. **Authentication failures**: Invalid or expired tokens
5. **Rate limits**: Too many requests
6. **Server errors**: 500 responses
7. **Network issues**: Timeouts, connection failures

## Publishing Your GPT

### Visibility Options

**Private:**
- Only you can access
- Good for testing
- No approval needed

**Anyone with link:**
- Shareable URL
- Not listed publicly
- Good for team/client sharing

**Public:**
- Listed in GPT store
- Searchable by anyone
- Requires review and approval

### GPT Store Guidelines

If publishing publicly:

**Requirements:**
- ✅ Useful and functional
- ✅ Clear description
- ✅ Appropriate name
- ✅ Working actions (if any)
- ✅ Follows OpenAI policies
- ❌ No spam or low-effort GPTs
- ❌ No policy violations
- ❌ No misleading descriptions

**Optimization:**
- Unique value proposition
- Professional icon/image
- Well-written instructions
- Tested thoroughly
- Good conversation starters
- Regular updates

## Common Patterns

### Pattern 1: API Wrapper GPT

Create a GPT that wraps an existing API:

**Instructions:**
```markdown
You are an expert assistant for [Service Name] API. You help users:
- Search and retrieve data
- Format API responses clearly
- Explain API capabilities
- Troubleshoot common issues

When responding:
1. Use the appropriate action
2. Format results in a readable way
3. Explain what was found
4. Offer next steps or related queries
```

**Actions:**
- Search/query endpoints
- Retrieve specific items
- Create/update operations (if applicable)

### Pattern 2: Data Analysis GPT

Analyze data using custom actions:

**Instructions:**
```markdown
You are a data analysis assistant. You:
- Fetch data from APIs
- Analyze trends and patterns
- Create visualizations (descriptions)
- Provide insights and recommendations

Always:
- Explain your methodology
- Show your work
- Cite data sources
- Acknowledge limitations
```

**Actions:**
- Fetch datasets
- Run aggregations
- Export results

### Pattern 3: Workflow Automation GPT

Orchestrate multiple API calls:

**Instructions:**
```markdown
You automate workflows by:
1. Understanding user goals
2. Breaking down into steps
3. Executing API calls in sequence
4. Handling errors gracefully
5. Reporting results clearly

Confirm before executing destructive operations.
```

**Actions:**
- Multiple CRUD operations
- Status checks
- Batch operations

## Debugging Common Issues

### Action Not Working

**Check:**
1. OpenAPI schema is valid (use validator)
2. Authentication is configured correctly
3. Server URL is correct and accessible
4. Parameter names match exactly
5. Response format matches schema
6. No CORS issues (for browser-based APIs)

**Debug steps:**
1. Test endpoint in Postman/curl
2. Check action logs in GPT settings
3. Verify schema against working example
4. Test with minimal parameters
5. Check server logs

### Authentication Failing

**Common causes:**
- Incorrect credential format
- Expired tokens
- Wrong authentication type
- Missing required headers
- CORS configuration

**Solutions:**
- Re-enter credentials
- Generate new API key
- Verify OAuth flow
- Check server logs
- Test authentication separately

### Poor Response Quality

**Improve with:**
- More detailed instructions
- Better examples in descriptions
- Clearer parameter descriptions
- Response format specifications
- Additional context in knowledge files

## Advanced Topics

### Function Calling vs Actions

**Function Calling** (via API):
- Programmatic GPT usage
- Full control over conversation
- Use in applications
- Can chain multiple calls

**Actions** (in Custom GPTs):
- User-facing GPTs
- Conversational interface
- No code required
- Limited to GPT platform

### Rate Limiting

Handle rate limits gracefully:

**In your API:**
```json
{
  "error": "Rate limit exceeded",
  "retry_after": 60,
  "limit": 100,
  "remaining": 0
}
```

**In GPT instructions:**
```markdown
If you encounter rate limits:
1. Inform the user
2. Suggest waiting
3. Offer alternative approaches
4. Don't retry immediately
```

### Webhooks and Async Operations

For long-running operations:

1. Return operation ID immediately
2. Provide status check endpoint
3. Offer polling mechanism
4. Consider webhook callbacks (if supported)

## Learn More

- **ChatGPT**: [chat.openai.com](https://chat.openai.com)
- **GPT Actions Guide**: [platform.openai.com/docs/actions](https://platform.openai.com/docs/actions)
- **OpenAPI Spec**: [spec.openapis.org](https://spec.openapis.org/oas/latest.html)
- **Function Calling**: [platform.openai.com/docs/guides/function-calling](https://platform.openai.com/docs/guides/function-calling)

## Quick Reference

**GPT Configuration:**
- Name: 3-5 words, clear function
- Description: 1-2 sentences
- Instructions: Detailed, with examples
- Starters: 4 example prompts

**Actions:**
- OpenAPI 3.0+ schema
- Clear operationId and descriptions
- Proper parameter types
- Authentication configured
- Tested thoroughly

**Best Practices:**
- Test extensively
- Handle errors gracefully
- Provide clear responses
- Secure authentication
- Follow OpenAI policies
