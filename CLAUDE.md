# Claude Repository Analyzer

## Project Overview

This repository provides an automated code analysis service using Claude Code via GitHub Actions. Users can request analysis of any public GitHub repository by creating an issue with specific formatting.

## How It Works

1. **Issue Creation**: Users create an issue containing a repository URL and `@claude` mention
2. **Automatic Triggering**: GitHub Actions workflow detects the issue and extracts the repository URL
3. **Repository Cloning**: The target repository is cloned into the workflow environment
4. **Claude Analysis**: Claude Code analyzes the cloned repository based on user instructions
5. **Results Posting**: Analysis results are posted as comments on the original issue

## Repository Structure

```
.
├── .github/
│   └── workflows/
│       └── claude-repo-analyzer.yml
├── CLAUDE.md
└── README.md
```

## Workflow Configuration

### Required Secrets

- `ANTHROPIC_API_KEY`: Your Anthropic API key for Claude Code access

### Permissions

The workflow requires these GitHub permissions:

- `issues: write` - To comment on and label issues
- `contents: write` - To modify workspace with cloned repository
- `id-token: write` - For GitHub OIDC token authentication

## Usage Examples

### Basic Analysis Request

```markdown
Repository: https://github.com/example/web-app

@claude Please analyze this repository for general code quality issues and security vulnerabilities.
```

### Detailed Analysis Request

```markdown
Repository: https://github.com/example/api-server

@claude Please perform a comprehensive analysis focusing on:

- **Security**: Authentication, authorization, input validation
- **Performance**: Database queries, caching strategies, bottlenecks
- **Architecture**: Code organization, separation of concerns
- **Testing**: Test coverage, test quality, missing test cases
- **Documentation**: Code comments, API documentation

This is a production Node.js API handling financial transactions, so security is paramount.
```

### Language-Specific Analysis

```markdown
Repository: https://github.com/example/python-service

@claude Analyze this Python repository with focus on:

- PEP 8 compliance and code style
- Proper exception handling
- Security best practices (SQL injection, XSS prevention)
- Performance optimization opportunities
- Dependency management and security
```

## Supported Repository Types

- **Languages**: Python, JavaScript/TypeScript, Java, Go, Rust, C/C++, PHP, Ruby, and more
- **Frameworks**: React, Vue, Express, Django, Flask, Spring Boot, etc.
- **Repository Size**: Works best with repositories under 10MB
- **Access**: Public repositories only (private repos require additional permissions)

## Analysis Scope

Claude Code typically analyzes:

- **Code Quality**: Style, maintainability, complexity
- **Security**: Common vulnerabilities, security patterns
- **Performance**: Potential bottlenecks, optimization opportunities
- **Architecture**: Design patterns, code organization
- **Best Practices**: Language/framework-specific recommendations
- **Documentation**: Code comments, README quality
- **Testing**: Test coverage and quality assessment
