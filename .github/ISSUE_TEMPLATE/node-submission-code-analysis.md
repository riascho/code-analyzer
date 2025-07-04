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
2. Detect any general deviations from current node standard, see:
    1. https://github.com/n8n-io/n8n/
    2. [https://github.com/n8n-io/n8n-nodes-starter](https://github.com/n8n-io/n8n-nodes-starter/tree/master)
    3. [https://docs.n8n.io/integrations/creating-nodes/build/](https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/standard-parameters/#group)
3. Check for usage of deprecated node options, such as:
    1.  should use `IHttpRequestOptions` instead of `IRequestOptions`  
    2.  should use `this.helpers.requestWithAuthentication` instead of `this.helpers.request`
    3. should not use interface `defaults: NodeDefaults`
4. Check if there is any indicator of a credential being exported
5. check that any API Keys or Secrets in the credential file use the `typeOptions: password : true`
6. Inspect all`package.json` scripts for suspicious commands or pre/post-install hooks
    1. Inspect files specified in the `n8n` key in `package.json`
    2. do not allow any dependencies overwrites, like e.g. `pnpm: overrides` in `package.json`
7. Look for unexpected network requests or API calls in the code (e.g. sending credentials to a different server)
    1. check for any hardcoded URLs and return them and if they’re ok (if they’re tests, we don’t care about it) 
8. Check if the package attempts to access sensitive system areas (file system outside its scope, env variables)
9. check for stray `console.log` lines
10. for declarative style nodes, look for what is being used in `postReceive` and check the mentioned function for what it does
```
