---
name: Node Submission Code Analysis
about: Describe this issue template's purpose here.
title: Code Analysis - NODE_NAME
labels: ''
assignees: ''

---

Repository: 

@claude Please perform the below Code Analysis:

1. Check for presence of obfuscated code or statements that could hide malicious behaviour, pay attention to the following:
    - Shouldn’t use globals
    - Shouldn’t use access to `process` (e.g. `process.env.`)
    - Shouldn’t use  `eval` and `Function()` .
    - Check that all http requests are valid and needed for the node
    - Check all `require/import` and make sure there aren’t any external items
        - should only import from n8n files and no external modules like `https`
2. Detect any general deviations from current node standard, see:
    a. https://github.com/n8n-io/n8n/
    b. [https://github.com/n8n-io/n8n-nodes-starter](https://github.com/n8n-io/n8n-nodes-starter/tree/master)
    c. [https://docs.n8n.io/integrations/creating-nodes/build/](https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/standard-parameters/#group)
3. Make sure all UI elements are in English and no other languages are used elsewhere in the code
4. Check for usage of deprecated node options, such as:
    a. should use `IHttpRequestOptions` instead of `IRequestOptions`  
    b. should use `this.helpers.requestWithAuthentication` instead of `this.helpers.request`
    c. should not use interface `defaults: NodeDefaults`
5. Check if there is any indicator of a credential being exported
6. check that any API Keys or Secrets in the credential file use the `typeOptions: password : true`
7. Inspect all`package.json` scripts for suspicious commands or pre/post-install hooks
    a. Inspect files specified in the `n8n` key in `package.json`
    b. do not allow any dependencies overwrites, like e.g. `pnpm: overrides` in `package.json`
    c. the following scripts are NOT allowed: 
        
        ```
        preinstall
        install
        postinstall
        prepublish
        preprepare
        prepare
        postprepare
        ```
   d. no unnecessary dependencies like `n8n-core` or `n8n-workflow` are allowed. 
8. Look for unexpected network requests or API calls in the code (e.g. sending credentials to a different server)
    a. check for any hardcoded URLs and return them and if they’re ok (if they’re tests, we don’t care about it) 
9. Check if the package attempts to access sensitive system areas (file system outside its scope, env variables)
10. check for stray `console.log` lines
11. for declarative style nodes, look for what is being used in `postReceive` and check the mentioned function for what it does
12. Make sure the node has proper error handling:
    a. errors should be handled using `NodeApiError` or `NodeOperationError`

Output only violations with reference to code lines and and keep your output below 2000 characters, give a result of `passed` or `failed`
