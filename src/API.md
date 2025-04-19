# APIs


A comprehensive collection of OpenAPI (Swagger) linting rules designed to enforce consistent API design practices. This repository provides multiple rulesets that can be used individually or combined to ensure your OpenAPI specifications follow best practices, maintain consistency, and adhere to security guidelines.

## Available Rulesets

### 1. Basic Ruleset (`basic.yaml`)
Provides fundamental validation rules by extending:
- `spectral:oas`: Core OpenAPI Specification rules
- `spectral:asyncapi`: AsyncAPI validation rules
- `spectral:arazzo`: Additional API design rules

### 2. Opinionated Ruleset (`opinionated.yaml`)
Extends the basic ruleset with additional style and documentation requirements:

#### Naming Conventions
- **Paths**: Must use kebab-case (e.g., `/user-profiles/active`)
- **Parameters**: Must use kebab-case (e.g., `user-id`, `account-status`)
- **JSON Keys**: Must use kebab-case in schema properties

#### Documentation Requirements
- All paths must include at least one example
- Request bodies should include examples (warning if missing)
- Response content should include examples (warning if missing)

### 3. OWASP Security Ruleset (`owasp.yaml`)
Incorporates OWASP security best practices using the `@stoplight/spectral-owasp-ruleset`.

## Getting Started

1. **Install Dependencies**:
   ```bash
   npm install -g @stoplight/spectral-cli
   ```

2. **Use the Ruleset**:
   ```bash
   # Basic validation
   spectral lint -r openapi/ruleset/basic.yaml your-api.yaml

   # Opinionated validation with style rules
   spectral lint -r openapi/ruleset/opinionated.yaml your-api.yaml

   # Security-focused validation
   spectral lint -r openapi/ruleset/owasp.yaml your-api.yaml
   ```

## Rule Examples

### Path Naming (kebab-case)
✅ Good:
```yaml
paths:
  /user-profiles:
  /active-sessions/{session-id}:
```

❌ Bad:
```yaml
paths:
  /userProfiles:
  /active_sessions/{sessionId}:
```

### Parameter Naming
✅ Good:
```yaml
parameters:
  - name: user-id
  - name: account-status
```

❌ Bad:
```yaml
parameters:
  - name: userId
  - name: accountStatus
```

### Required Examples
✅ Good:
```yaml
/users:
  get:
    responses:
      200:
        content:
          application/json:
            examples:
              success:
                value:
                  id: "123"
                  name: "John Doe"
```

## Contributing
1. Fork the repository
2. Create a feature branch
3. Submit a pull request with your changes
4. Ensure your changes include appropriate documentation

## License
This project is distributed under the [MIT License](LICENSE).
