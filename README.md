# launch-check

A CLI skill that validates your SaaS idea before you write a single line of code. It walks you through structured discovery, pressure-tests demand, scores your idea 1-10, and gives you a clear verdict: pursue, proceed with caution, or don't pursue.

Built for [Claude Code](https://docs.anthropic.com/en/docs/claude-code), and compatible with [OpenAI Codex CLI](https://github.com/openai/codex) and [Gemini CLI](https://github.com/google-gemini/gemini-cli).

## What It Does

**Phase 1 — Discovery**
- Detects B2B vs B2C and branches into the right question track
- B2C: value category, ICP with pricing, competitors, marketing channels with specific targets
- B2B: target customer, industry focus, revenue scalability, existing spend signal, competitors, first customer strategy

**Phase 2 — Validation**
- Checks 6 demand signals (pain described online, existing spend, forum requests, waitlist interest, complaints about alternatives)
- Scores the idea across 5 dimensions: Pain Clarity, Willingness to Pay, Market Size, Competition, Distribution Path
- Gives an overall score from 1-10 with detailed reasoning
- Recommends 2-3 validation methods you can run before building

**Phase 3 — Final Report**
- Structured markdown report with tables for ICP, competitors, channels, signals, and scores
- Optional PPTX slide deck export (9 slides, styled with verdict badges and color-coded scores)
- Offers to build the MVP with you after validation

## Setup

### Claude Code

1. Clone this repo into your Claude Code skills directory:

```bash
git clone https://github.com/TiyaaaJain/launch-check.git ~/.claude/skills/launch-check
```

Or if you already have a `~/.claude/skills/` directory, clone it there:

```bash
cd ~/.claude/skills
git clone https://github.com/TiyaaaJain/launch-check.git
```

2. That's it. Claude Code automatically detects skills in `~/.claude/skills/`. The skill will appear in your available skills list.

3. Run it:

```
/launch-check I want to build an AI tool that helps recruiters write better job descriptions
```

**For the PPTX export feature**, you need Node.js installed (for `npx`). The skill uses [Marp CLI](https://github.com/marp-team/marp-cli) to convert slides to PowerPoint. It installs automatically via `npx` when you request a deck — no manual setup needed.

### OpenAI Codex CLI

Codex CLI supports custom instructions via markdown files. To use this skill:

1. Clone the repo:

```bash
git clone https://github.com/TiyaaaJain/launch-check.git
```

2. Copy the skill file into your Codex instructions directory:

```bash
mkdir -p ~/.codex
cp launch-check/SKILL.md ~/.codex/launch-check.md
```

3. Reference it in your Codex configuration. Add to your `~/.codex/config.yaml` (or create one):

```yaml
instructions:
  - file: ~/.codex/launch-check.md
```

Alternatively, you can paste the contents of `SKILL.md` directly into your system prompt or instructions file.

4. Run Codex and provide your idea:

```
I want to validate a SaaS idea: an AI tool that helps recruiters write better job descriptions. Follow the launch-check skill instructions.
```

**Note:** Codex CLI does not have a `/slash-command` system like Claude Code. You invoke the skill by referencing it in your prompt or by including it in your instructions file. The PPTX export works the same way — Codex can run `npx` commands if it has shell access.

### Gemini CLI

Gemini CLI supports custom system instructions via markdown files. To use this skill:

1. Clone the repo:

```bash
git clone https://github.com/TiyaaaJain/launch-check.git
```

2. Copy the skill into your Gemini CLI configuration:

```bash
mkdir -p ~/.gemini
cp launch-check/SKILL.md ~/.gemini/launch-check.md
```

3. Reference it in your Gemini CLI settings. Add to your `~/.gemini/settings.json`:

```json
{
  "systemInstructions": "Follow the instructions in ~/.gemini/launch-check.md when the user asks to validate a SaaS idea."
}
```

Or load it directly as context when starting a session:

```bash
gemini --system-instruction "$(cat ~/.gemini/launch-check.md)"
```

4. Run it:

```
Validate my SaaS idea: an AI tool that helps recruiters write better job descriptions
```

**Note:** Gemini CLI does not have `/slash-commands`. Include the skill in your system instructions and reference it in your prompt. The PPTX export requires Node.js and works if Gemini CLI has shell/tool access enabled.

## Usage

Once installed, just provide your SaaS idea:

```
/launch-check [your idea here]
```

The skill will walk you through questions one at a time. Answer as much or as little as you want — it works with vague answers and skips questions you've already answered in your initial prompt.

At the end you get:
- A structured markdown report with verdict, scores, and next steps
- An optional PPTX slide deck
- An offer to start building the MVP

## Example Ideas to Test

```
/launch-check An AI-powered invoice management tool for freelancers
/launch-check A marketplace connecting local chefs with people who want home-cooked meals
/launch-check A Slack bot that summarizes long threads for engineering managers
/launch-check A browser extension that tracks price drops on B2B SaaS tools
```

## File Structure

```
launch-check/
  SKILL.md    # The skill definition (this is what the AI reads)
  README.md   # This file
```

## Requirements

- **For the skill itself:** Any AI CLI tool that supports custom instructions (Claude Code, Codex CLI, Gemini CLI)
- **For PPTX export:** Node.js 18+ (Marp CLI is installed automatically via `npx`)

## License

MIT
