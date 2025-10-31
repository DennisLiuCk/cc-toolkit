# CC Toolkit - Personal Claude Code Plugin Marketplace

A curated collection of personal Claude Code plugins designed to enhance development workflows, code quality, and collaborative problem-solving.

## What is This?

This repository serves as a personal marketplace for Claude Code plugins and skills. It allows you to:
- **Organize custom plugins** in one centralized location
- **Share plugins** across different projects and teams
- **Extend Claude Code** with custom commands, skills, and behaviors
- **Control your workflow** with specialized development tools
- **Enhance collaboration** through reflective dialogue and quality focus

## Quick Start

### 1. Add This Marketplace to Claude Code

```bash
/plugin marketplace add DennisLiuCk/cc-toolkit
```

### 2. Browse Available Plugins

```bash
# View all available plugins
/plugin
```

### 3. Install and Enable Plugins

```bash
# Install a plugin
/plugin install <plugin-name>@cc-toolkit

# Enable the plugin
/plugin enable <plugin-name>@cc-toolkit
```

### 4. Start Using

Plugins work automatically once enabled. Commands start with `/`, skills activate based on context, and hooks modify Claude's behavior.

## Available Plugins

### 🛠️ Dev Tools

**Type:** Commands + Skills
**Category:** Development
**Best for:** Daily development tasks, project analysis, code reviews

Essential development utilities for analyzing projects and reviewing code.

**Features:**
- **`/analyze-project`** - Comprehensive project structure and dependency analysis
- **Code Reviewer Skill** - Automatically activates for code review requests

**When to use:**
- Starting work on a new codebase
- Performing code reviews
- Understanding project architecture
- Checking for code quality issues

**Installation:**
```bash
/plugin install dev-tools@cc-toolkit
/plugin enable dev-tools@cc-toolkit
```

**Example:**
```bash
# Analyze your project
/analyze-project

# Or just ask for a code review
"Can you review this function for security issues?"
```

[📖 Full Documentation →](./plugins/dev-tools/README.md)

---

### ✓ Code Quality Focus

**Type:** SessionStart Hook
**Category:** Development
**Best for:** Production code, security-sensitive applications, maintaining high standards

Automatically emphasizes code quality, best practices, and clean code principles throughout your session.

**Features:**
- **Quality Check Summaries** - After implementing code, shows quality validations
- **SOLID Principles** - Encourages proper design patterns
- **Security Focus** - Highlights input validation, injection prevention
- **Performance Awareness** - Points out efficiency considerations
- **Testability** - Promotes dependency injection and mockable code

**When to use:**
- Writing production code
- Security-sensitive applications
- Learning best practices
- Code that will be maintained by a team
- When quality matters more than speed

**Output Format:**
```
✓ Quality Check ────────────────────────────────
- Applied Single Responsibility: Separated validation from logic
- Input sanitization added to prevent SQL injection
- Used dependency injection for easier testing
- Function kept under 20 lines for readability
────────────────────────────────────────────────
```

**Installation:**
```bash
/plugin install code-quality-focus@cc-toolkit
/plugin enable code-quality-focus@cc-toolkit
```

**Token Cost:** ⚠️ Moderate to High - Adds quality insights throughout session

[📖 Full Documentation →](./plugins/code-quality-focus/README.md)

---

### 💭 Reflective Dialogue Style

**Type:** SessionStart Hook
**Category:** Productivity
**Best for:** Learning, complex design decisions, collaborative problem-solving

Transforms Claude into a conversational, reflective partner who explains motivations with examples, regularly reflects on progress, and actively discusses design decisions.

**Features:**
- **💡 Conversational Explanations** - Uses natural language with concrete examples
- **💭 Reflection Checkpoints** - Pauses to discuss direction and potential issues
- **🤔 Proactive Discussion** - Asks questions when discovering trade-offs
- **✨ Iterative Design** - Refines approach based on your feedback
- **📚 Teaching Through Examples** - Uses analogies and comparisons

**When to use:**
- Learning new technologies or patterns
- Designing complex systems
- Need to understand "why" not just "what"
- Collaborative decision-making
- Exploring different approaches
- Teaching or knowledge transfer

**Example Interaction:**

**Without plugin:**
> User: "Create a user login function"
> Claude: [writes code]

**With plugin:**
> User: "Create a user login function"
>
> Claude: "Let me explain my thinking here. I'm creating a secure login function with:
>
> 1. **Password hashing** - Never store plain text passwords
> 2. **SQL injection prevention** - Using parameterized queries
> 3. **Rate limiting** - Prevent brute force attacks
>
> For example, if an attacker tries to guess passwords, rate limiting locks the account after 5 failed attempts for 15 minutes.
>
> [Implements code]
>
> 💭 Reflection Checkpoint ───────────────────────
>
> I've built basic login, but I'm noticing: what about password reset? Should we add that now or later?
>
> Also, for session management: JWT tokens or server-side sessions? Each has trade-offs. Let's discuss...
> ────────────────────────────────────────────────"

**Installation:**
```bash
/plugin install reflective-dialogue-style@cc-toolkit
/plugin enable reflective-dialogue-style@cc-toolkit
```

**Token Cost:** ⚠️ High - Very conversational and detailed

[📖 Full Documentation →](./plugins/reflective-dialogue-style/README.md)

---

## Plugin Comparison

### Quick Comparison Table

| Plugin | Type | Interaction Level | Token Cost | Best Use Case |
|--------|------|------------------|------------|---------------|
| **Dev Tools** | Commands + Skills | Low (on-demand) | Low | Daily development tasks |
| **Code Quality Focus** | SessionStart Hook | Medium (automatic insights) | Medium-High | Production code development |
| **Reflective Dialogue** | SessionStart Hook | High (conversational) | High | Learning & complex design |

### Detailed Comparison

| Feature | Dev Tools | Code Quality Focus | Reflective Dialogue |
|---------|-----------|-------------------|---------------------|
| **Activation** | Manual command or skill trigger | Automatic (entire session) | Automatic (entire session) |
| **Output Style** | Standard analysis | ✓ Quality Check format | 💭 💡 ✨ Conversational |
| **Explanations** | When requested | Quality-focused | Detailed with examples |
| **User Interaction** | Passive (receives output) | Passive (receives checks) | Active (discussions) |
| **Design Iteration** | No | No | Yes (based on feedback) |
| **Teaching Focus** | Minimal | Medium | High |
| **Code Examples** | Limited | Medium | Rich with analogies |
| **Reflection Points** | No | No | Yes (regular checkpoints) |
| **Best for Beginners** | ✓ Good | ○ Medium | ✓✓ Excellent |
| **Best for Experts** | ✓✓ Excellent | ✓✓ Excellent | ✓ Good |
| **Speed** | ✓✓ Fast | ✓ Moderate | ○ Slower (more thorough) |

### When to Use Each Plugin

#### Use **Dev Tools** when:
- ✅ You need to analyze a project structure
- ✅ You want quick code review feedback
- ✅ You're comfortable with standard output
- ✅ You want minimal token usage
- ✅ You need on-demand tools

#### Use **Code Quality Focus** when:
- ✅ Writing production code
- ✅ Working on security-sensitive features
- ✅ Learning best practices
- ✅ Need constant quality reminders
- ✅ Want to maintain high standards
- ❌ NOT for quick prototypes or experiments

#### Use **Reflective Dialogue** when:
- ✅ Learning new concepts or technologies
- ✅ Designing complex systems
- ✅ Want to understand trade-offs deeply
- ✅ Need collaborative decision-making
- ✅ Teaching or knowledge transfer
- ❌ NOT for simple, straightforward tasks
- ❌ NOT when token cost is a primary concern

### Combining Plugins

You can enable multiple plugins simultaneously:

**Good Combinations:**
- **Dev Tools + Code Quality Focus** - Daily development with quality emphasis
- **Dev Tools + Reflective Dialogue** - Learn while building
- All three together for comprehensive support (but high token cost)

**Avoid:**
- **Code Quality Focus + Reflective Dialogue** together - May be overly verbose

## Repository Structure

```
cc-toolkit/
├── .claude-plugin/
│   └── marketplace.json              # Marketplace configuration
├── plugins/
│   ├── dev-tools/                    # Commands + Skills plugin
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   └── analyze-project.md
│   │   ├── skills/
│   │   │   └── code-reviewer/
│   │   │       └── SKILL.md
│   │   └── README.md
│   │
│   ├── code-quality-focus/           # SessionStart Hook plugin
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── hooks/
│   │   │   └── hooks.json
│   │   ├── hooks-handlers/
│   │   │   └── session-start.sh      # The magic happens here
│   │   └── README.md
│   │
│   └── reflective-dialogue-style/    # SessionStart Hook plugin
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── hooks/
│       │   └── hooks.json
│       ├── hooks-handlers/
│       │   └── session-start.sh      # Conversational instructions
│       └── README.md
│
├── .gitignore
├── LICENSE
└── README.md                         # This file
```

## Understanding Plugin Types

### Commands

Slash commands you invoke manually:
- Defined in `commands/*.md` files
- Invoked with `/command-name`
- Example: `/analyze-project`

### Skills

Auto-activating based on context:
- Defined in `skills/*/SKILL.md` files
- Claude chooses when to use them
- Example: Code reviewer skill activates when you ask for code review

### SessionStart Hooks

Modify Claude's behavior for entire session:
- Defined in `hooks-handlers/session-start.sh`
- Inject additional instructions at session start
- Example: Code Quality Focus adds quality emphasis

**How SessionStart Hooks Work:**
1. Session starts
2. Hook script executes
3. Script outputs JSON with `additionalContext`
4. Context is injected into Claude's instructions
5. Claude follows these instructions throughout session

## Creating Your Own Plugins

### Plugin Structure Templates

#### Basic Plugin (Commands + Skills)
```
plugins/your-plugin/
├── .claude-plugin/
│   └── plugin.json              # Required: Plugin metadata
├── commands/                     # Optional: Slash commands
│   └── command-name.md
├── skills/                       # Optional: Auto-activating skills
│   └── skill-name/
│       └── SKILL.md
└── README.md                    # Plugin documentation
```

#### SessionStart Hook Plugin
```
plugins/your-plugin/
├── .claude-plugin/
│   └── plugin.json
├── hooks/
│   └── hooks.json               # Register the hook
├── hooks-handlers/
│   └── session-start.sh         # Hook implementation
└── README.md
```

### Adding a New Plugin

1. **Create plugin directory** in `plugins/`
   ```bash
   mkdir -p plugins/my-plugin/.claude-plugin
   ```

2. **Create plugin.json** with metadata
   ```json
   {
     "name": "my-plugin",
     "description": "What this plugin does",
     "version": "1.0.0",
     "author": {
       "name": "Your Name",
       "email": "your.email@example.com"
     },
     "keywords": ["keyword1", "keyword2"]
   }
   ```

3. **Create plugin components**
   - Add commands in `commands/`
   - Add skills in `skills/`
   - Add hooks if needed

4. **Register in marketplace.json**
   ```json
   {
     "name": "my-plugin",
     "description": "What this plugin does",
     "version": "1.0.0",
     "source": "./plugins/my-plugin",
     "category": "development",
     "keywords": ["keyword1", "keyword2"]
   }
   ```

5. **Commit and push** to GitHub

6. **Update in Claude Code**
   ```bash
   /plugin marketplace update cc-toolkit
   ```

### Example: Creating a SessionStart Hook Plugin

See [code-quality-focus](./plugins/code-quality-focus) or [reflective-dialogue-style](./plugins/reflective-dialogue-style) as examples.

**Key files:**

**hooks/hooks.json:**
```json
{
  "description": "Hook description",
  "hooks": {
    "SessionStart": [
      {
        "command": "${CLAUDE_PLUGIN_ROOT}/hooks-handlers/session-start.sh"
      }
    ]
  }
}
```

**hooks-handlers/session-start.sh:**
```bash
#!/bin/bash
cat <<'EOF'
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "Your instructions here..."
  }
}
EOF
exit 0
```

## Team Usage

### Automatic Installation for Teams

Add to `.claude/settings.json` in your project:

```json
{
  "extraKnownMarketplaces": {
    "cc-toolkit": {
      "source": {
        "source": "github",
        "repo": "DennisLiuCk/cc-toolkit"
      }
    }
  },
  "plugins": {
    "dev-tools@cc-toolkit": {
      "enabled": true
    },
    "code-quality-focus@cc-toolkit": {
      "enabled": true
    }
  }
}
```

Team members will automatically get the plugins when they trust the repository folder.

### Recommended Team Configurations

**For Production Teams:**
```json
{
  "plugins": {
    "dev-tools@cc-toolkit": { "enabled": true },
    "code-quality-focus@cc-toolkit": { "enabled": true }
  }
}
```

**For Learning/Training:**
```json
{
  "plugins": {
    "dev-tools@cc-toolkit": { "enabled": true },
    "reflective-dialogue-style@cc-toolkit": { "enabled": true }
  }
}
```

**For Individual Exploration:**
```json
{
  "plugins": {
    "reflective-dialogue-style@cc-toolkit": { "enabled": true }
  }
}
```

## Configuration

Before using, update the following with your information:

### .claude-plugin/marketplace.json
- `owner.name` - Your name
- `owner.email` - Your email
- `owner.url` - Your GitHub repository URL
- `plugins[].author` - Author info for each plugin

### plugins/*/.claude-plugin/plugin.json
- `author.name` - Your name
- `author.email` - Your email
- `homepage` - Your repository URL (if applicable)
- `repository` - Your repository URL (if applicable)

## Maintenance

### Updating Plugins

1. Make changes to plugin files
2. Update version in `plugin.json` (follow semver)
3. Update version in `marketplace.json`
4. Update CHANGELOG if you have one
5. Commit and push changes
6. Users run `/plugin marketplace update cc-toolkit` to get updates

### Versioning

Follow semantic versioning (semver):
- `1.0.0` - Initial release
- `1.0.1` - Bug fixes (backward compatible)
- `1.1.0` - New features (backward compatible)
- `2.0.0` - Breaking changes

### Testing Plugins Locally

Before pushing to GitHub:

```bash
# Install from local path
/plugin install ./plugins/your-plugin

# Test functionality
# Make adjustments
# Uninstall when done
/plugin uninstall your-plugin
```

## Troubleshooting

### Plugin Not Showing Up
- Check `marketplace.json` syntax (must be valid JSON)
- Ensure plugin is registered in `plugins` array
- Run `/plugin marketplace update cc-toolkit`
- Check plugin name matches directory name

### SessionStart Hook Not Working
- Verify `hooks.json` exists and is valid
- Check `session-start.sh` is executable (`chmod +x`)
- Ensure script outputs valid JSON
- Try restarting Claude Code session

### Plugin Too Verbose
- This is expected for SessionStart hooks like Reflective Dialogue
- Consider disabling for simple tasks
- Use `/plugin disable <plugin-name>@cc-toolkit` temporarily

### Conflicts Between Plugins
- Some SessionStart hooks may conflict
- Try enabling one at a time
- Disable plugins you're not actively using

## Resources

### Official Documentation
- [Claude Code Documentation](https://docs.claude.com/en/docs/claude-code)
- [Plugin Development Guide](https://docs.claude.com/en/docs/claude-code/plugins)
- [Skill Development Guide](https://docs.claude.com/en/docs/claude-code/skills)
- [Hook System Documentation](https://docs.claude.com/en/docs/claude-code/hooks)

### Example Plugins
- [Anthropic's Official Plugins](https://github.com/anthropics/claude-code/tree/main/plugins)
- [Explanatory Output Style](https://github.com/anthropics/claude-code/tree/main/plugins/explanatory-output-style) - Inspiration for this marketplace

### Community
- [Claude Code GitHub](https://github.com/anthropics/claude-code)
- [Report Issues](https://github.com/anthropics/claude-code/issues)

## Best Practices

### Plugin Development
1. **Keep plugins focused** - One clear purpose per plugin
2. **Write clear descriptions** - Users should understand what it does
3. **Provide examples** - Show real usage in README
4. **Test thoroughly** - Try with different prompts and scenarios
5. **Document token costs** - Be transparent about verbosity
6. **Use semantic versioning** - Help users understand changes

### Using Plugins
1. **Start with one** - Don't enable all plugins at once
2. **Understand token costs** - SessionStart hooks increase usage
3. **Disable when not needed** - Save tokens for simple tasks
4. **Read the documentation** - Each plugin has specific use cases
5. **Experiment** - Try different combinations to find what works

### Hook Development
1. **Output valid JSON** - Hook scripts must return proper JSON
2. **Keep instructions focused** - Don't try to do too much
3. **Provide format examples** - Show Claude expected output format
4. **Balance verbosity** - Give guidance on when to be detailed
5. **Test thoroughly** - Ensure hooks behave as expected

## FAQ

**Q: Can I use multiple SessionStart hooks at once?**
A: Yes, but they may make Claude very verbose. Try one at a time first.

**Q: How much do these plugins cost in tokens?**
A: Dev Tools is minimal. Code Quality Focus is moderate. Reflective Dialogue is high.

**Q: Can I modify the plugins?**
A: Absolutely! Fork this repo and customize to your needs.

**Q: Do plugins work offline?**
A: Plugins are local files, but Claude Code requires internet connection.

**Q: Can I distribute my plugins to others?**
A: Yes! Share your marketplace repo URL and others can add it.

**Q: How do I uninstall a plugin?**
A: `/plugin uninstall plugin-name@cc-toolkit`

**Q: What's the difference between skills and commands?**
A: Commands are manual (`/command`). Skills activate automatically based on context.

**Q: Can I create plugins for other Claude products?**
A: Skills work across Claude products. Plugins and hooks are Claude Code specific.

## License

MIT License - Feel free to fork and customize for your own use.

See [LICENSE](./LICENSE) file for details.

## Author

**Dennis Liu**
- GitHub: [@DennisLiuCk](https://github.com/DennisLiuCk)
- Email: nossi1970@gmail.com

## Contributing

Contributions welcome! To improve this marketplace:

1. Fork the repository
2. Create a feature branch
3. Add or improve plugins
4. Test thoroughly
5. Submit a pull request with clear description

## Support

For issues or questions:

1. Check the [Claude Code documentation](https://docs.claude.com/en/docs/claude-code)
2. Review individual plugin README files
3. Open an issue in this repository
4. Check the [FAQ](#faq) section above

## Changelog

### v1.0.0 (2025-01-01)
- Initial release
- Added dev-tools plugin (commands + skills)
- Added code-quality-focus plugin (SessionStart hook)
- Added reflective-dialogue-style plugin (SessionStart hook)
- Complete marketplace structure
- Comprehensive documentation

---

**Happy coding with enhanced Claude Code capabilities!**
