# screenshot-review

Claude Code skill that sends screenshots to GitHub Copilot CLI (GPT-5.4) for UI review.

Claude Code cannot view images. This skill bridges that gap by delegating visual review to GPT-5.4 via the GitHub Copilot CLI.

## How it works

```
Claude Code (code generation)
    ↓ takes screenshot
    ↓ copilot CLI
GitHub Copilot / GPT-5.4 (image review)
    ↓ feedback
Claude Code (applies fixes)
```

## Prerequisites

- [GitHub Copilot CLI](https://docs.github.com/copilot/how-tos/copilot-cli) installed and authenticated
- Claude Code

## Installation

Copy `SKILL.md` into your project's `.claude/skills/screenshot-review/` directory:

```bash
mkdir -p .claude/skills/screenshot-review
cp SKILL.md .claude/skills/screenshot-review/
```

Then ask Claude Code to review your UI:

```
"screenshot review this screen"
"UI review して"
"GPTに見せて"
```

## Usage examples

### Single image review

Claude Code runs:

```bash
copilot -p "@./screenshots/screen.png Review this UI..." --allow-all --model gpt-5.4 -s
```

### Before/After comparison

```bash
copilot -p "@before.png @after.png Compare these two versions..." --allow-all --model gpt-5.4 -s
```

## License

MIT
