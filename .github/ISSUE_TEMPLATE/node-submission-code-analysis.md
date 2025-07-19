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
  - Shouldn't use globals
  - Shouldn't use access to `process` (e.g. `process.env.`)
  - Shouldn't use `eval` and `Function()`
  - Check that all HTTP requests are valid and needed for the node
  - Check all `require/import` and make sure there aren't any external items
    - Should only import from n8n files and no external modules like `https`

**8. Network Security & API Calls**

- Look for unexpected network requests or API calls in the code (e.g. sending credentials to a different server)
- Check for any hardcoded URLs and return them and if they're ok (if they're tests, we don't care about it)

**9. System Access & Credentials**

- Check if the package attempts to access sensitive system areas (file system outside its scope, env variables)
- Check if there is any indicator of a credential being exported
- Check that any API Keys or Secrets in the credential file use the `typeOptions: password : true`

### 📋 N8N Standards & Compliance

**2. Node Standards Validation** (Reference: `n8n-nodes-starter/`)

- Detect any general deviations from current node standard, see:
  - https://github.com/n8n-io/n8n/
  - [https://github.com/n8n-io/n8n-nodes-starter](https://github.com/n8n-io/n8n-nodes-starter/tree/master)
  - [https://docs.n8n.io/integrations/creating-nodes/build/](https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/standard-parameters/#group)

**4. Deprecated API Usage**

- Check for usage of deprecated node options, such as:
  - Should use `IHttpRequestOptions` instead of `IRequestOptions`
  - Should use `this.helpers.requestWithAuthentication` instead of `this.helpers.request`

**3. Localization Requirements**

- Make sure all UI elements are in English and no other languages are used elsewhere in the code

### 📦 Package.json Security Analysis

**7. Package Scripts & Dependencies**

- Inspect all `package.json` scripts for suspicious commands or pre/post-install hooks
  - Inspect files specified in the `n8n` key in `package.json`
  - Do not allow any dependencies overwrites, like e.g. `pnpm: overrides` in `package.json`
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
  - No unnecessary dependencies like `n8n-core` or `n8n-workflow` are allowed.

### 🛠 Code Quality & Best Practices

**10-12. Development Standards**

- Check for stray `console.log` lines
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
