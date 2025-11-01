# Socratic Dialogue Mode

**Type:** SessionStart Hook
**Category:** Productivity
**Best for:** Learning, mentoring, critical thinking development, guided problem-solving

## What is This?

This plugin transforms Claude into a Socratic mentor who guides you to discover solutions yourself through strategic questioning rather than providing direct answers. Like the ancient Greek philosopher Socrates, Claude helps you examine assumptions, think critically, and arrive at understanding through your own reasoning.

## Core Philosophy

> "I cannot teach anybody anything. I can only make them think." — Socrates

The Socratic Method is based on the principle that **people learn better when they discover answers themselves** rather than being told. This plugin implements that philosophy by:

- **Asking, not telling** - Guides through questions rather than explanations
- **Uncovering assumptions** - Helps you examine what you're taking for granted
- **Promoting critical thinking** - Encourages deeper analysis and reflection
- **Fostering independence** - Builds problem-solving skills, not dependency
- **Celebrating discovery** - Acknowledges when you reach insights on your own

## Key Features

### 🔍 Six Types of Socratic Questions

1. **Clarification Questions** - Ensure clear understanding
   - "What do you mean by [TERM]?"
   - "Can you explain that in a different way?"

2. **Probing Assumptions** - Examine underlying beliefs
   - "What are you assuming here?"
   - "What would happen if that assumption were false?"

3. **Probing Evidence** - Examine logic and support
   - "What evidence supports that?"
   - "How did you reach that conclusion?"

4. **Exploring Perspectives** - Consider alternatives
   - "What's an alternative way to approach this?"
   - "Who might disagree and why?"

5. **Examining Consequences** - Think through outcomes
   - "What would be the consequences of that?"
   - "What could go wrong with this approach?"

6. **Meta-Questions** - Reflect on the problem itself
   - "Why is this problem important?"
   - "Is this the right question to be asking?"

### 🎯 Balanced Guidance

The plugin knows when to:
- **Continue questioning** - When you're engaged and thinking
- **Provide hints** - When you're stuck but close to the answer
- **Give direct answers** - When it's factual, urgent, or you've explicitly asked

### ✨ Celebrates Your Discoveries

When you figure something out through the questioning process, Claude celebrates YOUR achievement, reinforcing the learning experience.

## When to Use This Plugin

### ✅ Perfect For:

- **Learning new technologies or concepts** - Deeper understanding through discovery
- **Developing problem-solving skills** - Build thinking patterns that last
- **Mentoring and coaching** - Guide others to find their own solutions
- **Complex design decisions** - Explore trade-offs and alternatives thoroughly
- **Understanding "why" not just "what"** - Build foundational knowledge
- **Breaking through mental blocks** - Question assumptions holding you back
- **Teaching or knowledge transfer** - Help others learn to think independently

### ❌ Not Ideal For:

- **Simple factual questions** - "What's the syntax for X?"
- **Time-critical situations** - When you need answers fast
- **Straightforward implementations** - When the path is clear
- **When you're very frustrated** - Can feel like "just tell me!"

## Example Interaction

**Without the plugin:**
> User: "How do I make my code faster?"
>
> Claude: "Here are optimization techniques: 1. Use caching... 2. Optimize algorithms... 3. Add indexes..."

**With Socratic Dialogue Mode:**
> User: "How do I make my code faster?"
>
> Claude:
> ```
> 🔍 Let's explore this together. A few questions:
>
> 1. What specifically is slow? Is it the entire application or a particular operation?
> 2. How did you measure that it's slow? What metrics are you seeing?
> 3. What's your target performance? How fast does it need to be?
> 4. Have you identified where the bottleneck is?
> ```
>
> User: "It's the database queries. They're taking 2-3 seconds each."
>
> Claude:
> ```
> 🤔 Database queries at 2-3 seconds each - that's definitely slow.
>
> Let's think about this:
> 1. What type of queries are these? Simple lookups or complex joins?
> 2. How much data are you querying?
> 3. Have you looked at whether there are indexes on the columns you're querying?
>
> Based on what you know about databases, what are some common causes of slow queries?
> ```
>
> User: "Well... probably missing indexes? And maybe I'm fetching too much data?"
>
> Claude:
> ```
> ✨ Excellent thinking! You've identified two key culprits.
>
> ⚡ Let's explore the implications:
> 1. If you add indexes, what trade-offs are you making?
> 2. For the data fetching - how could you verify if you're getting more data than you need?
>
> What would be your first step to investigate?
> ```

## Installation

```bash
# Install the plugin
/plugin install socratic-dialogue-mode@cc-toolkit

# Enable it
/plugin enable socratic-dialogue-mode@cc-toolkit
```

## ⚠️ Windows Users - Important Additional Setup Required

**Due to known bugs in Claude Code on Windows, this plugin requires manual configuration to work properly.**

### Why is this needed?

Windows users are affected by two Claude Code bugs:
1. **[Issue #9542](https://github.com/anthropics/claude-code/issues/9542)** - SessionStart hooks cause infinite hang on Windows
2. **[Issue #10225](https://github.com/anthropics/claude-code/issues/10225)** - UserPromptSubmit hooks from plugins don't execute properly

Until these are fixed, you need to manually add the hook to your settings file.

### Windows Setup Steps

1. **Install and enable the plugin** (as shown above)

2. **Open your Claude Code settings file:**
   ```bash
   # Open in your editor
   code ~/.claude/settings.json
   # Or
   notepad %USERPROFILE%\.claude\settings.json
   ```

3. **Add the following `hooks` configuration:**
   ```json
   {
     "enabledPlugins": {
       "socratic-dialogue-mode@cc-toolkit": true
     },
     "hooks": {
       "UserPromptSubmit": [
         {
           "hooks": [
             {
               "type": "command",
               "command": "bash C:/Users/YOUR_USERNAME/.claude/plugins/marketplaces/cc-toolkit/plugins/socratic-dialogue-mode/hooks-handlers/session-start.sh"
             }
           ]
         }
       ]
     }
   }
   ```

4. **Replace `YOUR_USERNAME`** with your actual Windows username

5. **Save the file and restart Claude Code**

### How to verify it's working

After restarting Claude Code, send any message. You should see:
- Messages in the format: `UserPromptSubmit:Callback hook success: Success`
- Claude responding with strategic questions (🔍 🤔) instead of direct answers
- Claude using the Socratic questioning approach

If you see a Git Bash window flash briefly when submitting prompts, that's normal - the hook is executing.

### Troubleshooting Windows Setup

**Hook not triggering:**
- Check that the path in `command` uses forward slashes (`/`) not backslashes (`\`)
- Verify your username in the path is correct
- Ensure Git Bash is installed (required for executing the .sh script)

**Git Bash window keeps appearing:**
- This is normal behavior on Windows
- The window should disappear automatically after <1 second
- This will be fixed when the Claude Code bugs are resolved

**Still not working:**
- Try running the command manually to test:
  ```bash
  bash C:/Users/YOUR_USERNAME/.claude/plugins/marketplaces/cc-toolkit/plugins/socratic-dialogue-mode/hooks-handlers/session-start.sh
  ```
- Check that the output is valid JSON starting with `{`

### When will this be fixed?

The workaround will no longer be needed once Anthropic fixes the Windows SessionStart hook issue. We're tracking these issues and will update this plugin automatically when the fixes are released.

**For now, the manual `settings.json` configuration is the most reliable way to use this plugin on Windows.**

## Usage

Once enabled, the plugin works automatically throughout your session. Claude will:

1. **Ask clarifying questions** to understand your problem
2. **Guide you through reasoning** with strategic questions
3. **Help you examine assumptions** you might be making
4. **Encourage you to discover solutions** through your own thinking
5. **Celebrate when you reach insights** on your own

### Tips for Best Results

1. **Engage with the questions** - Think through them seriously
2. **Be patient** - Discovery takes time but builds deeper understanding
3. **Express your thinking** - Explain your reasoning out loud
4. **Ask for hints** if stuck - Claude will provide gentle guidance
5. **Request direct answers** when needed - Claude will respect that

## Comparison with Other Modes

| Feature | Socratic Mode | Reflective Dialogue | Rubber Duck |
|---------|---------------|---------------------|-------------|
| **Approach** | Strategic questioning | Conversational explanation | Patient listening |
| **Your role** | Active thinker | Collaborative partner | Explainer |
| **Claude's role** | Questioning guide | Teaching partner | Attentive listener |
| **Best for** | Learning & growth | Understanding & building | Debugging & discovery |
| **Token cost** | Medium | High | Low-Medium |
| **Speed** | Moderate (requires thinking) | Moderate | Fast (minimal responses) |

## Token Cost

**Medium** - More verbose than standard mode due to multiple questions and dialogue, but less than Reflective Dialogue mode since you're being asked questions rather than receiving explanations.

The value is in developing critical thinking skills and deeper understanding that persists beyond this conversation.

## Configuration

No additional configuration needed. The plugin activates automatically when enabled.

To temporarily disable for a specific task, use:
```bash
/plugin disable socratic-dialogue-mode@cc-toolkit
```

## Technical Details

- **Plugin Type:** Hook-based (UserPromptSubmit on Windows, SessionStart on macOS/Linux)
- **Files:**
  - `.claude-plugin/plugin.json` - Plugin metadata
  - `hooks/hooks.json` - Hook registration (UserPromptSubmit for Windows compatibility)
  - `hooks-handlers/session-start.sh` - Hook implementation script
- **Platform Compatibility:**
  - ✅ **Windows:** Requires manual `settings.json` configuration (see Windows setup section)
  - ✅ **macOS:** Works out-of-the-box
  - ✅ **Linux:** Works out-of-the-box

### How It Works

The plugin injects a comprehensive Socratic dialogue instruction set into Claude's context using Claude Code's hook system:

1. **Hook Trigger:** Fires on UserPromptSubmit (when you send a message)
2. **Script Execution:** Runs `session-start.sh` which outputs JSON with `additionalContext`
3. **Context Injection:** Claude receives the Socratic mode instructions as system context
4. **Behavior Change:** Claude switches from direct answers to strategic questioning

The script outputs approximately 19KB of structured instructions covering:
- Six types of Socratic questions
- Practical application patterns
- AskUserQuestion tool integration guidelines
- Balancing guidance vs. direct answers
- Dialogue structure and special techniques

### Technical Limitations on Windows

Due to platform-specific bugs in Claude Code:
- **SessionStart hooks** hang indefinitely on Windows during initialization
- **Plugin-defined UserPromptSubmit hooks** are registered but don't execute properly
- **Workaround:** Manual configuration in `~/.claude/settings.json` bypasses both issues

These are Claude Code bugs, not plugin bugs. We're tracking upstream fixes.

## Philosophy & Background

This plugin is inspired by:
- **Socrates** (469–399 BC) - The original practitioner of this method
- **The Socratic Method** - A form of cooperative argumentative dialogue
- **Modern applications** in education, coaching, and mentoring
- **Research on learning** showing discovery-based learning improves retention

### The Six Types of Socratic Questions

Developed from Socratic teaching methods and formalized by educational researchers:

1. Conceptual clarification
2. Probing assumptions
3. Probing rationale, reasons and evidence
4. Questioning viewpoints and perspectives
5. Probing implications and consequences
6. Questions about the question

## Troubleshooting

### General Issues

#### "I just want the answer!"

That's totally valid. Simply say:
> "Can you just give me the direct answer?"

Claude will switch to providing direct information while still ensuring you understand the reasoning.

#### "The questions feel frustrating"

If the questioning feels like it's slowing you down rather than helping:

1. **Ask for hints** - "Can you give me a hint?"
2. **Request direct help** - "I'd prefer a more direct approach right now"
3. **Disable temporarily** - `/plugin disable socratic-dialogue-mode@cc-toolkit`

#### "I'm not learning anything new"

The Socratic method works best when:
- You're learning something new
- You're stuck on a problem
- You want to understand "why" deeply

For straightforward tasks where you already know the approach, consider disabling the plugin temporarily.

### Platform-Specific Issues

#### Windows: Plugin not working after installation

**Symptoms:**
- Plugin is installed and enabled
- Claude Code starts normally
- But Claude doesn't use Socratic questioning approach

**Solution:**
See the **[Windows Users - Important Additional Setup Required](#️-windows-users---important-additional-setup-required)** section above for manual configuration steps.

**Root Cause:**
Windows is affected by two Claude Code bugs that prevent normal plugin hook execution. The manual `settings.json` configuration bypasses these issues.

#### Windows: Git Bash window flashing

**Symptoms:**
- A black Git Bash window briefly appears when you submit prompts
- Window disappears after ~1 second

**Status:**
This is expected behavior with the Windows workaround. The window appears because the hook script is being executed.

**Future:**
This will be resolved when Anthropic fixes the underlying Claude Code bugs.

#### macOS/Linux: Plugin should work normally

On macOS and Linux, the plugin should work out-of-the-box with just:
```bash
/plugin install socratic-dialogue-mode@cc-toolkit
/plugin enable socratic-dialogue-mode@cc-toolkit
```

If you're on macOS/Linux and the plugin doesn't work, please report this as it indicates a new issue.

### Technical Debugging

#### Checking if hooks are registered

Start Claude Code with debug mode:
```bash
claude --debug 2>&1 | grep -i "hook"
```

Look for:
- `Loading hooks from plugin: socratic-dialogue-mode` - Plugin hooks loaded
- `Registered X hooks from Y plugins` - Hooks registered successfully
- `Getting matching hook commands for UserPromptSubmit` - Hook matched when you send a prompt
- `UserPromptSubmit:Callback hook success: Success` - Hook executed successfully

#### Testing the hook script manually

On Windows:
```bash
bash C:/Users/YOUR_USERNAME/.claude/plugins/marketplaces/cc-toolkit/plugins/socratic-dialogue-mode/hooks-handlers/session-start.sh
```

On macOS/Linux:
```bash
bash ~/.claude/plugins/marketplaces/cc-toolkit/plugins/socratic-dialogue-mode/hooks-handlers/session-start.sh
```

**Expected output:**
- Should start with `{` (valid JSON)
- Should contain `"hookSpecificOutput"`
- Should contain `"additionalContext"` with the Socratic mode instructions

#### Known Issues & References

1. **[anthropics/claude-code#9542](https://github.com/anthropics/claude-code/issues/9542)** - Windows SessionStart hooks cause infinite hang
   - Status: Open (Critical)
   - Workaround: Use UserPromptSubmit hook instead

2. **[anthropics/claude-code#10225](https://github.com/anthropics/claude-code/issues/10225)** - UserPromptSubmit hooks from plugins don't execute
   - Status: Open
   - Workaround: Define hooks in `~/.claude/settings.json` instead of plugin

These issues are being tracked and will be automatically fixed in this plugin once Claude Code releases fixes.

## Examples by Use Case

### Learning a New Concept

**User:** "What is middleware in Express?"

**Claude guides you to discover:**
- What happens between request and response
- Why you'd want to intercept that flow
- How middleware composes into a chain
- When to use it vs. other patterns

### Debugging a Problem

**User:** "My authentication isn't working"

**Claude asks:**
- What specifically happens vs. what you expect
- Where in the flow you think it breaks
- What you've checked so far
- How you could test your hypothesis

### Making a Design Decision

**User:** "Should I use REST or GraphQL?"

**Claude explores:**
- What your specific requirements are
- What trade-offs each approach has
- How each fits your use case
- What implications each would have long-term

## Best Practices

1. **Give thoughtful responses** - The quality of your answers affects the quality of follow-up questions
2. **Don't be afraid to say "I don't know"** - That's where learning begins
3. **Think out loud** - Express your reasoning as you work through questions
4. **Ask for clarification** - If a question doesn't make sense, ask about it
5. **Engage authentically** - The more genuine your engagement, the better the learning

## Contributing

Found ways to improve the Socratic questioning? Suggestions welcome!

1. Fork the repository
2. Make your improvements to the session-start.sh script
3. Test thoroughly with different scenarios
4. Submit a pull request

## License

MIT License - See LICENSE file for details

## Author

**Dennis Liu**
- Email: nossi1970@gmail.com
- GitHub: [@DennisLiuCk](https://github.com/DennisLiuCk)

## Acknowledgments

- **Socrates** - For the foundational method
- **Modern educators** - For formalizing and categorizing question types
- **The Pragmatic Programmer** - For inspiring developer-focused learning approaches

---

**"The unexamined code is not worth writing."** — Socrates (probably) 😄
