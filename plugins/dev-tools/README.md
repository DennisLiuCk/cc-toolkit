# Dev Tools Plugin

A collection of essential development tools and utilities for Claude Code, designed to enhance your daily coding workflows.

## Features

### Commands

#### `/analyze-project`
Performs a comprehensive analysis of your current project, including:
- Project structure and organization
- Dependencies and versions
- Code organization patterns
- Development setup
- Documentation status

**Usage:**
```bash
/analyze-project
```

### Skills

#### Code Reviewer
Automatically activates when you need code review assistance. Provides thorough analysis covering:
- Code quality and readability
- Best practices and design patterns
- Security vulnerabilities
- Performance optimization
- Testing coverage
- Documentation

**Trigger phrases:**
- "Review this code"
- "Can you check this PR?"
- "What do you think about this implementation?"

## Installation

### From Marketplace
```bash
/plugin install dev-tools@cc-toolkit
```

### Manual Installation
```bash
/plugin marketplace add DennisLiuCk/cc-toolkit
/plugin install dev-tools@cc-toolkit
```

## Usage Examples

### Analyzing a Project
```bash
/analyze-project
```

Claude will scan your project and provide:
- Executive summary
- Detailed findings per category
- Recommendations for improvements
- Suggested next steps

### Getting Code Review
Simply mention you want a review:
```
Can you review this function for security issues?

def login(username, password):
    query = f"SELECT * FROM users WHERE username='{username}' AND password='{password}'"
    return db.execute(query)
```

The code-reviewer skill will activate and provide comprehensive feedback.

## Requirements

- Claude Code CLI
- Git repository (for project analysis features)

## License

MIT License - See LICENSE file for details

## Author

Dennis Liu

## Contributing

This plugin is part of the cc-toolkit personal marketplace. Feel free to fork and customize for your own needs.
