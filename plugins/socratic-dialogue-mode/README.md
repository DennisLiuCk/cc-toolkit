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

- **Plugin Type:** SessionStart Hook
- **Files:**
  - `.claude-plugin/plugin.json` - Plugin metadata
  - `hooks/hooks.json` - Hook registration
  - `hooks-handlers/session-start.sh` - SessionStart hook implementation

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

### "I just want the answer!"

That's totally valid. Simply say:
> "Can you just give me the direct answer?"

Claude will switch to providing direct information while still ensuring you understand the reasoning.

### "The questions feel frustrating"

If the questioning feels like it's slowing you down rather than helping:

1. **Ask for hints** - "Can you give me a hint?"
2. **Request direct help** - "I'd prefer a more direct approach right now"
3. **Disable temporarily** - `/plugin disable socratic-dialogue-mode@cc-toolkit`

### "I'm not learning anything new"

The Socratic method works best when:
- You're learning something new
- You're stuck on a problem
- You want to understand "why" deeply

For straightforward tasks where you already know the approach, consider disabling the plugin temporarily.

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
