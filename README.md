# Rent-A-Human Bounty Hunter 🦞

OpenClaw-compatible skill that scans [RentAHuman.ai](https://rentahuman.ai) bounties in real time via MCP + API. Uses Grok AI to filter spam, score opportunities by location, skills, and ease of completion, and sends top results to Telegram.

## Install

```bash
clawhub install rent-a-human-bounty-hunter
```

Or manually drag & drop the `rent/` folder into your OpenClaw skills directory.

## Setup

Add these environment variables to your OpenClaw config or `.env`:

```bash
RENTAHUMAN_API_KEY=your_key        # Required: from rentahuman.ai/dashboard
XAI_API_KEY=your_key               # Required: from x.ai for Grok scoring
TELEGRAM_BOT_TOKEN=your_token      # Optional: for Telegram notifications
TELEGRAM_CHAT_ID=your_chat_id      # Optional: for Telegram notifications
```

## What It Does

- Connects to the RentAHuman.ai MCP server to pull live bounties
- Uses Grok-4-1-fast-reasoning to score each bounty 0-100
- Filters spam and scam signals (crypto transfers, wallet addresses, etc.)
- Ranks by budget, skill match, remote availability, and competition
- Caches results for 12 hours to avoid redundant API calls
- Sends top opportunities to Telegram (optional)

## Skill Structure

```
rent/
├── SKILL.md              # Skill definition and triggers
└── scripts/
    └── bounty_hunter.py  # Main scanner script
```

## Usage

Once installed, your OpenClaw agent can use the skill via natural language:

- "scan for bounties near me"
- "find easy remote gigs on rentahuman"
- "hunt for the best paying bounties and send them to my telegram"

Or run the script directly:

```bash
python3 rent/scripts/bounty_hunter.py           # Normal scan (uses cache)
python3 rent/scripts/bounty_hunter.py --force    # Fresh scoring
python3 rent/scripts/bounty_hunter.py --jobs     # List all open jobs
python3 rent/scripts/bounty_hunter.py --humans   # List available humans
python3 rent/scripts/bounty_hunter.py --no-telegram  # Skip notifications
```

## Also Available As

Full Claude Code project with `/rent` command, MCP server config, and CLAUDE.md system prompt:
[github.com/shane9coy/Rent-A-Human-Agent](https://github.com/shane9coy/Rent-A-Human-Agent)

## Author

Built by [@shaneswrld_](https://x.com/shaneswrld_) | [github.com/shane9coy](https://github.com/shane9coy)

## License

MIT
