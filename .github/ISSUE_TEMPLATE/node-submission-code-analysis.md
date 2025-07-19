---
name: N8N Node Security Analysis
about: Submit an N8N node for comprehensive security and compliance analysis
title: "N8N Node Analysis - [NODE_NAME]"
labels: ""
assignees: ""
---

## Repository Information

**Repository:** https://github.com/OWNER/REPOSITORY_NAME

## Analysis Request

@claude Please perform comprehensive N8N Node security and compliance analysis with the following requirements:

### 🔒 Security & Malicious Code Detection

**1. Obfuscated Code & Dangerous Patterns**

- Check for presence of obfuscated code or statements that could hide malicious behaviour, pay attention to the following:
  - Should not use globals
  - Should not use access to `process` (e.g. `process.env.`)
  - Should not use `eval` and `Function()`
  - all HTTP requests should be valid and needed for the node
  - Check all `require/import` and make sure there aren't any external items
    - Should only import from n8n files and no external modules like `https`

**8. Network Security & API Calls**

- there should be no unexpected network requests or API calls in the code (e.g. sending credentials to a different server)
- find and return any hardcoded URLs (if they're tests, we don't care about it)

**9. System Access & Credentials**

- package should not attempt to access sensitive system areas (file system outside its scope, env variables)
- there should not be any indicator of a credential being exported
- any API Keys or Secrets in the credential file should use the `typeOptions: password : true`

### 📋 N8N Standards & Compliance

**2. Node Standards Validation** (Reference: `n8n-nodes-starter/`)

- compare the `./cloned-repo` with the base line repo `./n8n-nodes-starter` and detect any deviations in terms of structure and especially in the `package.json`.

**4. Deprecated API Usage**

- Check for usage of deprecated node options, such as:
  - Should use `IHttpRequestOptions` instead of `IRequestOptions`
  - Should use `this.helpers.requestWithAuthentication` instead of `this.helpers.request`

**3. Localization Requirements**

- Make sure all UI elements are in English and no other languages are used elsewhere in the code (comments don't matter)

### 📦 Package.json Security Analysis

**7. Package Scripts & Dependencies**

- `package.json` scripts should not contain any suspicious commands or pre/post-install hooks
- The following scripts are NOT allowed:
  ```
  preinstall
  install
  postinstall
  prepublish
  preprepare
  prepare
  postprepare
  ```
- Inspect files specified in the `n8n` key in `package.json`
- Do not allow any dependencies overwrites, like `pnpm: overrides`
- No unnecessary dependencies like `n8n-core` or `n8n-workflow` are allowed.

### 🛠 Code Quality & Best Practices

**10-12. Development Standards**

- there should not be any stray `console.log` lines
- For declarative style nodes, look for what is being used in `postReceive` and check the mentioned function for what it does
- Make sure the node has proper error handling:
  - Errors should be handled using `NodeApiError` or `NodeOperationError`

## Expected Output Format

Please provide your analysis in the following structured format:

### Security Analysis Result: `PASSED` or `FAILED`

### Summary

Brief overview of findings (2-3 sentences)

### Violations Found

Only list actual violations with specific file paths and line numbers:

- **File:** `path/to/file.js:line_number`
- **Issue:** Description of the violation
- **Severity:** High/Medium/Low

### Recommendations

- Key security improvements needed
- Code compliance suggestions

**Note:** Keep total output under 2000 characters for optimal readability.
