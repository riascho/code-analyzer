---
name: Node Submission Code Analysis
about: Describe this issue template's purpose here.
title: Code Analysis - {{ NODE }}
labels: ''
assignees: ''

---

Repository: __________

```
@claude Please perform the below Code Analysis:
1. Check for presence of obfuscated code or statements that could hide malicious behaviour, pay attention to the following:
    - Check that it doesn’t use globals
    - Check that it doesn’t use access to `process`.
    - Check that it doesn’t use  `eval` and `Function()` .
    - Check all http requests are valid and needed for the node
    - Check all `require/import` and make sure there aren’t any forbidden items there
2. Detect any general deviations from current node standard (see https://github.com/n8n-io/n8n/)
3. Check for usage of deprecated node options, such as:
    1.  using `IRequestOptions` instead of `IHttpRequestOptions`  
    2. using interface `defaults: NodeDefaults`
    3.  using `this.helpers.request` instead of `this.helpers.requestWithAuthentication`
4. Check if there is any indicator of a credential being exported in both npm and github
5. check that any API Keys or Secrets in the credential file use the `typeOptions: password : true`
6. Inspect files specified in the `n8n` key in `package.json`
7. Inspect all`package.json` scripts for suspicious commands or pre/post-install hooks
    - do not allow any dependencies overwrites, like e.g. `pnpm: overrides` in `package.json`
8. Check if the package attempts to access sensitive system areas (file system outside its scope, env variables)
9. Look for unexpected network requests or API calls in the code
    - check for any hardcoded URLs and return them and if they’re ok (if they’re tests, we don’t care about it)
10. check for stray `console.log` lines
```
