# screenshot-review

AI coding agent skill that delegates image review to GPT-5.4 via GitHub Copilot CLI.

Most AI coding agents (Claude Code, GitHub Copilot CLI, etc.) have limited image understanding compared to GPT-5.4. This skill bridges that gap by sending screenshots to GPT-5.4 for visual review.

## How it works

```
AI coding agent (code generation)
    ↓ takes screenshot
    ↓ copilot CLI
GitHub Copilot / GPT-5.4 (image review)
    ↓ feedback
AI coding agent (applies fixes)
```

## Prerequisites

- [GitHub Copilot CLI](https://docs.github.com/copilot/how-tos/copilot-cli) installed and authenticated

## Installation

Copy `SKILL.md` into your project's skills directory. For Claude Code:

```bash
mkdir -p .claude/skills/screenshot-review
cp SKILL.md .claude/skills/screenshot-review/
```

For GitHub Copilot CLI, place it as `AGENTS.md` or reference it in your agent instructions.

Then ask your AI agent to review your UI:

```
"screenshot review this screen"
"UI review して"
"GPTに見せて"
```

## Usage examples

### Single image review

```bash
copilot -p "@./screenshots/screen.png Review this UI..." --allow-all --model gpt-5.4 -s
```

### Before/After comparison

```bash
copilot -p "@before.png @after.png Compare these two versions..." --allow-all --model gpt-5.4 -s
```

## License

MIT
