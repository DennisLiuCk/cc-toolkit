# Code Quality Focus Plugin

A Claude Code plugin that automatically emphasizes code quality, best practices, and clean code principles throughout your development sessions.

## What It Does

This plugin uses a `SessionStart` hook to inject additional instructions at the beginning of each Claude Code session. Once activated, Claude will:

1. Proactively highlight quality considerations after implementing code
2. Apply SOLID principles and clean code practices
3. Emphasize security, performance, and testability
4. Provide "Quality Check" summaries using a distinctive format
5. Suggest refactoring opportunities when code smells are detected

## Output Format

When the plugin is active, you'll see quality insights formatted like this:

```
✓ Quality Check ────────────────────────────────
- Applied Single Responsibility: Separated validation from business logic
- Input sanitization added to prevent SQL injection attacks
- Used dependency injection for easier testing
- Function kept under 20 lines for better readability
────────────────────────────────────────────────
```

## Focus Areas

The plugin emphasizes:

- **SOLID Principles**: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
- **Clean Code**: Meaningful names, small functions, clear intent
- **Error Handling**: Comprehensive and informative error management
- **Security**: Input validation, injection prevention, authentication checks
- **Performance**: Algorithm efficiency, resource management, query optimization
- **Testability**: Dependency injection, pure functions, mockable dependencies
- **Maintainability**: DRY principle, consistent patterns, separation of concerns

## Installation

### From Marketplace

```bash
# Add the cc-toolkit marketplace (if not already added)
/plugin marketplace add DennisLiuCk/cc-toolkit

# Install the plugin
/plugin install code-quality-focus@cc-toolkit

# Enable the plugin
/plugin enable code-quality-focus@cc-toolkit
```

### Manual Installation

If you have the repository locally:

```bash
/plugin install ./plugins/code-quality-focus
```

## Usage

Once installed and enabled, the plugin activates automatically at the start of each session. There are no commands to run - Claude will simply be more proactive about code quality.

### Example Interaction

**You:** Create a user login function

**Claude:** I'll create a user login function with security and quality in mind.

```python
def login_user(username: str, password: str, db_connection: DatabaseConnection) -> LoginResult:
    """
    Authenticate user credentials and return login result.

    Args:
        username: User's username (will be sanitized)
        password: User's password (will be hashed)
        db_connection: Database connection for queries

    Returns:
        LoginResult with success status and user data or error message
    """
    # Validate inputs
    if not username or not password:
        return LoginResult(success=False, error="Username and password required")

    # Sanitize username to prevent SQL injection
    sanitized_username = sanitize_input(username)

    # Hash password for comparison
    password_hash = hash_password(password)

    # Use parameterized query
    query = "SELECT * FROM users WHERE username = ? AND password_hash = ?"
    result = db_connection.execute(query, (sanitized_username, password_hash))

    if result:
        return LoginResult(success=True, user=result)

    return LoginResult(success=False, error="Invalid credentials")
```

✓ Quality Check ────────────────────────────────
- Input validation prevents empty credentials
- SQL injection prevented via parameterized queries
- Passwords never stored or compared in plain text
- Dependency injection used (db_connection) for testability
- Clear return types and error messages
- Function has single responsibility (authentication only)
────────────────────────────────────────────────

## When to Use This Plugin

**Good for:**
- Production code development
- Code reviews and refactoring sessions
- Learning best practices
- Security-sensitive applications
- Team projects requiring high code quality

**Consider disabling for:**
- Quick prototypes or experiments
- Learning exercises where you want minimal guidance
- Performance-critical tasks where verbosity matters
- Simple scripts or one-off utilities

## Token Cost Consideration

**Important:** This plugin increases token usage because Claude will provide additional quality insights and explanations. The extra output is valuable for learning and maintaining code quality, but it does consume more tokens.

**Do not install this plugin unless you are comfortable with the additional token cost.**

## Management

### Check Status

```bash
/plugin
```

Look for `code-quality-focus@cc-toolkit` in the list.

### Temporarily Disable

```bash
/plugin disable code-quality-focus@cc-toolkit
```

This keeps the plugin installed but inactive. Re-enable with:

```bash
/plugin enable code-quality-focus@cc-toolkit
```

### Uninstall Completely

```bash
/plugin uninstall code-quality-focus@cc-toolkit
```

### Customize for Your Needs

1. Fork or clone the repository
2. Edit `hooks-handlers/session-start.sh` to modify the instructions
3. Install your customized version locally:
   ```bash
   /plugin install /path/to/your/customized/plugin
   ```

## How It Works

This plugin uses the **SessionStart hook** mechanism:

1. When a Claude Code session starts, hooks registered for `SessionStart` are executed
2. The plugin's `session-start.sh` script outputs JSON with `additionalContext`
3. This context is injected into Claude's instructions for the entire session
4. Claude follows these instructions throughout the conversation

### File Structure

```
code-quality-focus/
├── .claude-plugin/
│   └── plugin.json              # Plugin metadata
├── hooks/
│   └── hooks.json               # Hook registration
├── hooks-handlers/
│   └── session-start.sh         # Hook script (the magic happens here)
└── README.md                    # This file
```

## Comparison to Explanatory Output Style

This plugin is inspired by the built-in [Explanatory Output Style](https://github.com/anthropics/claude-code/tree/main/plugins/explanatory-output-style) plugin but focuses specifically on **code quality** rather than general educational insights.

| Feature | Explanatory Style | Code Quality Focus |
|---------|-------------------|-------------------|
| Purpose | Educational insights | Code quality emphasis |
| Focus | Implementation choices, patterns | SOLID, security, clean code |
| Output Format | ★ Insight | ✓ Quality Check |
| Use Case | Learning about codebases | Writing production-quality code |

## Combining with Other Plugins

This plugin works well alongside:
- **dev-tools** plugin (from this marketplace) - for project analysis
- **test-focused** plugins - complementary testing emphasis
- **documentation** plugins - quality code + quality docs

## Troubleshooting

### Plugin not activating
- Verify it's enabled: `/plugin`
- Check for conflicts with other SessionStart hooks
- Try restarting Claude Code

### Too verbose
- This is expected behavior - the plugin adds quality insights
- Consider disabling for simpler tasks
- Customize the script to reduce verbosity

### Not enough quality checks
- The plugin activates based on code complexity
- Simple tasks may not trigger quality checks
- Claude adapts to the task - production code gets more scrutiny

## Technical Details

- **Hook Type:** SessionStart
- **Execution:** Once per session initialization
- **Scope:** Affects entire session until restart
- **Performance Impact:** Minimal (hook runs once at start)
- **Token Impact:** Moderate to high (additional output throughout session)

## License

MIT License - Same as the cc-toolkit marketplace

## Author

Dennis Liu

## Contributing

To improve this plugin:
1. Fork the cc-toolkit repository
2. Make changes to the plugin files
3. Test thoroughly
4. Submit a pull request with detailed description

## Version History

- **1.0.0** (2025-01-01)
  - Initial release
  - SessionStart hook implementation
  - Quality Check format
  - SOLID principles focus
  - Security and performance emphasis
