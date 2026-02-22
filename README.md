# Arbitrum Skills

An LLM skill that provides AI assistants with comprehensive, up-to-date knowledge of the Arbitrum ecosystem. Instead of relying on training data that may be outdated or incomplete, this skill gives LLMs direct access to official documentation, smart contract source code, and API references.

## What Is This?

LLM skills are structured knowledge bases that AI coding assistants read at query time. When you ask an Arbitrum-related question, the assistant reads the relevant files from this skill and constructs an accurate, source-cited answer — instead of guessing from potentially outdated training data.

### Why It Matters

| Without Skill | With Skill |
|--------------|------------|
| `stylus-sdk 0.6.0` (wrong) | `stylus-sdk 0.9.0` (correct) |
| `sol_storage!` macro (deprecated) | `#[storage]` + `#[entrypoint]` (current) |
| `@arbitrum/orbit-sdk` (old name) | `@arbitrum/chain-sdk` (current) |
| On-chain `submitBid()` (wrong architecture) | Offchain `auctioneer_submitBid` JSON-RPC (correct) |
| 8-16 GB RAM for full node (4x underestimate) | 64 GB RAM (correct) |
| 5-13 uncertainty flags per answer | 0 uncertainties, every claim cited |

In a controlled A/B test across 6 questions, the skill improved average response quality from **5.3/10 to 8.8/10** (+66%).

## Installation

### One-Command Install

```bash
npx skills add utkucy/arbitrum-skills
```

### Manual Install

```bash
# Clone
git clone https://github.com/utkucy/arbitrum-skills.git

# Copy to your LLM's skills directory (example: Claude Code)
cp -r arbitrum-skills ~/.claude/skills/
```

## What's Included

### Documentation

Parsed from the official [Arbitrum documentation](https://docs.arbitrum.io/):

| Topic | Covers |
|-------|--------|
| Launch Arbitrum Chain | Orbit deployment, custom gas tokens, DAC setup, AnyTrust/Rollup |
| For Devs | Chain IDs, RPC endpoints, dev frameworks, tools |
| Build Decentralized Apps | Solidity/Stylus quickstart, cross-chain messaging, oracles, token bridging |
| Run Arbitrum Node | Full node, archive, validator, sequencer, troubleshooting |
| Stylus | WASM contracts in Rust, SDK, CLI tools, testing |
| How Arbitrum Works | Nitro internals, BoLD, Timeboost, gas/fees, AnyTrust |
| Other | Bridge, SDK, glossary, audit reports, notices |

### Smart Contract Source Code

Parsed from 3 official repositories:

| Repository | Content |
|-----------|---------|
| [OpenZeppelin Stylus](https://github.com/OpenZeppelin/rust-contracts-stylus) | ERC-20/721/1155, access control, proxy patterns, finance utilities |
| [Stylus SDK](https://github.com/OffchainLabs/stylus-sdk-rs) | Storage, ABI encoding, proc macros, host I/O, testing framework |
| [Nitro Contracts](https://github.com/OffchainLabs/nitro-contracts) | Bridge (Inbox/Outbox), rollup management, BoLD challenge protocol |

### Navigation Structure

```
arbitrum-skills/
├── SKILL.md                    # Entry point (222 lines) — decision guide + topic map
├── NAV-docs.md                 # Full documentation index
├── NAV-smart-contracts.md      # Smart contract repos overview
├── NAV-openzeppelin-stylus.md  # OpenZeppelin Stylus contracts index
├── NAV-stylus-sdk.md           # Stylus SDK source index
├── NAV-nitro-contracts.md      # Nitro contracts index
├── stylus/                     # Stylus WASM development
├── build-decentralized-apps/   # dApp building guides
├── run-arbitrum-node/          # Node operations
├── launch-arbitrum-chain/      # Orbit chain deployment
├── how-arbitrum-works/         # Architecture deep-dives
├── smart-contracts/            # Source code from 3 repos
│   ├── openzeppelin-stylus/
│   ├── stylus-sdk/
│   └── nitro-contracts/
└── ...
```

The skill uses **progressive disclosure**: the 222-line `SKILL.md` entry point routes the LLM to the right files via a Decision Guide, so it only reads what's relevant to the question — typically 10-14 file reads per query.

## Updating

```bash
cd ~/.claude/skills/arbitrum-skills
git pull origin main
```

No build step required — the skill is just files.

## Related Projects

| Project | Description | Link |
|---------|-------------|------|
| **Arbitrum Skills** | This repo — the generated LLM skill | [GitHub](https://github.com/utkucy/arbitrum-skills) |
| **Arbitrum Skill Generator** | CLI tool that generates this skill from source | [GitHub](https://github.com/utkucy/arbitrum-skill-generator) |
| **Arbitrum MCP Tools** | MCP tools for blockchain operations (deploy, query, analyze) | [GitHub](https://github.com/utkucy/arbitrum-mcp-tools) |
| **Documentation** | Full documentation for all projects | [GitBook](https://arbitrum-ai-hub.gitbook.io/docs) |

## License

MIT
