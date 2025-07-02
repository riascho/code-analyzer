# code-analyzer

## Overview

This repository provides an automated code analysis service using Claude Code via GitHub Actions. Users can request analysis of any public GitHub repository by creating an issue with a specific format.

## How It Works

1. **Issue Creation**: Create a GitHub issue containing a repository URL and your instruction in a `@claude` mention.
2. **Automatic Triggering**: The GitHub Actions workflow detects the issue and extracts the repository URL.
3. **Repository Cloning**: The target repository is cloned into the workflow environment.
4. **Claude Analysis**: Claude Code analyzes the cloned repository based on user instructions.
5. **Results Posting**: Analysis results are posted as comments on the original issue.

## Requirements

1. Install [Claude Code Actions](https://github.com/apps/claude) from GitHub Marketplace
2. Configure repository secrets:
   - Get your API key from [Anthropic Console](https://console.anthropic.com/)
   - Add `ANTHROPIC_API_KEY` to your repository's GitHub Secrets

## Usage

To request an analysis, open a new issue in this repository and include the following in the issue body:

```markdown
Repository: https://github.com/example/repo

@claude Please analyze this repository for code quality and security issues.
```

## Restrictions

For security and resource management reasons, only specifically allowed GitHub accounts can trigger the analysis workflow. If you're interested in using this service but aren't currently authorized, please contact the repository maintainers for access.
