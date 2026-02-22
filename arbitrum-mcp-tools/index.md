# Arbitrum MCP Tools

# Overview

## Arbitrum MCP Tools 🚀🦾

This project provides a set of tools for interacting with the Arbitrum blockchain via the Model Context Protocol (MCP), enabling AI assistants like Claude Desktop, Claude Code, Cursor, Windsurf, VS Code, Gemini CLI, Antigravity, and OpenAI Codex to perform blockchain operations.

### Table of Contents 📚

* [Overview](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/readme)
* [Setup Guide](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/setup-guide)
* [Project Structure](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/project-structure)
* [Network Tools](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/network-mcp-tools)
  * [Account Analysis](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/network-mcp-tools/account-analysis)
  * [Batch Operations](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/network-mcp-tools/batch-operations)
  * [Chain Data](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/network-mcp-tools/chain-data)
  * [Contract Interaction](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/network-mcp-tools/contract-interaction)
  * [Cross Chain](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/network-mcp-tools/cross-chain-operations)
  * [Development](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/network-mcp-tools/development)
* [Stylus MCP Tools](https://arbitrum-mcp-tools.gitbook.io/arbitrum-mcp-tools-docs/stylus-mcp-tools)


# Setup Guide 🛠️

## Prerequisites

* Node.js v20.x or higher
* npm (comes with Node.js)
* Alchemy API Key (sign up at <https://www.alchemy.com/>)
* Arbiscan API Key (optional, sign up at <https://arbiscan.io>) - Required for the `decodeTransactionCalldata` tool

## Quick Start

The fastest way to get started is using the universal CLI installer:

```bash
npx arbitrum-mcp-tools install
```

This launches an interactive wizard that guides you through the setup process.

## Supported Platforms

Arbitrum MCP Tools supports **8 platforms** across macOS, Windows, and Linux:

| Platform       | Format | Global Config Location                          |
| -------------- | ------ | ----------------------------------------------- |
| Claude Desktop | JSON   | `~/Library/Application Support/Claude/` (macOS) |
| Claude Code    | JSON   | `~/.claude.json`                                |
| Cursor         | JSON   | `~/.cursor/mcp.json`                            |
| Windsurf       | JSON   | `~/.codeium/windsurf/mcp_config.json`           |
| VS Code        | JSON   | `~/.vscode/mcp.json`                            |
| Gemini CLI     | JSON   | `~/.gemini/settings.json`                       |
| Antigravity    | JSON   | `~/.gemini/antigravity/mcp_config.json`         |
| OpenAI Codex   | TOML   | `~/.codex/config.toml`                          |

## Installation Wizard

When you run `npx arbitrum-mcp-tools install`, the wizard will guide you through:

### 1. Platform Selection

Select one or more platforms to install:

```
? Select platforms to install: (Press <space> to select)
❯ ◯ Claude Desktop
  ◯ Claude Code
  ◯ Cursor
  ◯ Windsurf
  ◯ VS Code
  ◯ Gemini CLI
  ◯ Antigravity
  ◯ OpenAI Codex
```

### 2. Scope Selection

Choose between global and local installation for each platform:

* **Global**: Installs to your user-level config (available in all projects)
* **Local**: Installs to the current project directory (project-specific)

### 3. Post-Installation

After installation completes:

1. Set up your environment variables (see below)
2. Restart your AI assistant application
3. The Arbitrum MCP tools will be available automatically

## Environment Variables Setup

The MCP tools require API keys to function. Set these in your shell profile:

### macOS / Linux

Add to `~/.zshrc` or `~/.bashrc`:

```bash
# Required
export ALCHEMY_API_KEY="your_alchemy_api_key_here"

# Optional (for transaction decoding)
export ARBISCAN_API_KEY="your_arbiscan_api_key_here"

# Stylus Contract Authentication (choose one)
# Option 1: Direct private key
export STYLUS_PRIVATE_KEY="your_private_key_here"

# Option 2: Path to private key file
export STYLUS_PRIVATE_KEY_PATH="/path/to/your/private/key/file"

# Option 3: Path to keystore file
export STYLUS_KEYSTORE_PATH="/path/to/your/keystore/file"
```

Then reload your shell:

```bash
source ~/.zshrc  # or source ~/.bashrc
```

### Windows (PowerShell)

```powershell
# Set environment variables permanently
[Environment]::SetEnvironmentVariable("ALCHEMY_API_KEY", "your_alchemy_api_key_here", "User")
[Environment]::SetEnvironmentVariable("ARBISCAN_API_KEY", "your_arbiscan_api_key_here", "User")

# For Stylus (choose one method)
[Environment]::SetEnvironmentVariable("STYLUS_PRIVATE_KEY", "your_private_key_here", "User")
```

Restart your terminal after setting environment variables.

## CLI Commands

### install

Interactive installation wizard for setting up MCP tools.

```bash
npx arbitrum-mcp-tools install
```

### uninstall

Interactive wizard to remove MCP tools from selected platforms.

```bash
npx arbitrum-mcp-tools uninstall
```

### list

Display all supported platforms and their current installation status.

```bash
npx arbitrum-mcp-tools list
```

### --help

Show help information and available commands.

```bash
npx arbitrum-mcp-tools --help
```

### --version

Display the current version.

```bash
npx arbitrum-mcp-tools --version
```

### serve

Start the MCP server. This command is used internally by MCP clients and typically not run directly by users.

```bash
npx arbitrum-mcp-tools serve
```

## How It Works

When you install Arbitrum MCP Tools, the CLI adds a configuration entry to your AI assistant's config file. This configuration tells the assistant to run the MCP server using:

```json
{
  "command": "npx",
  "args": ["-y", "arbitrum-mcp-tools", "serve"]
}
```

This means:

* The MCP server is always fetched from npm (no local installation required)
* Updates are automatic when you restart your AI assistant
* The same configuration works across all platforms and operating systems

## Troubleshooting

### Tools not appearing in AI assistant

1. Ensure you've restarted the application after installation
2. Verify environment variables are set correctly: `echo $ALCHEMY_API_KEY`
3. Run `npx arbitrum-mcp-tools list` to check installation status
4. Check the config file was created in the expected location

### Permission errors on macOS/Linux

If you encounter permission errors, ensure you have write access to the config directory:

```bash
# For global configs
ls -la ~/.cursor/
ls -la ~/.claude.json
```

### Windows path issues

On Windows, ensure paths use forward slashes or escaped backslashes in config files.

### Config file conflicts

If you have existing MCP configurations, the installer will merge them (not overwrite). To start fresh:

1. Run `npx arbitrum-mcp-tools uninstall`
2. Delete the config file manually if needed
3. Run `npx arbitrum-mcp-tools install` again

### Getting help

For additional support:

* GitHub Issues: <https://github.com/utkucy/arbitrum-mcp-tools/issues>
* Documentation: <https://utkucy.gitbook.io/arbitrum-mcp-tools>


# Project Structure

The codebase is organized into modular components:

```
src/
├── index.ts                # Entry point (runs server)
├── server.ts               # MCP server setup and Alchemy config
├── cli/                    # CLI installer
│   ├── index.ts            # CLI entry point
│   ├── commands/           # CLI commands (install, uninstall, list, serve)
│   ├── clients/            # Platform config generators
│   └── utils/              # CLI utilities
├── tools/                  # All tools organized by category
│   ├── common.ts           # Shared utilities and configs
│   ├── index.ts            # Tool registration
│   ├── accountAnalysis/    # Account analysis tools
│   ├── chainData/          # Chain data tools
│   ├── contractInteraction/# Contract interaction tools
│   ├── crossChain/         # Cross-chain tools
│   ├── development/        # Development tools
│   ├── batchOperations/    # Batch operation tools
│   └── stylus/             # Stylus development tools
```

#### Adding New Tools 🛠️

**Arbitrum MCP Tools uses an active registration pattern** – every tool is registered at runtime with `server.tool(...)`. To add a new tool you need to:

1. **Add the tool to its category’s `registerXTools` function**

```typescript
// src/tools/myCategory/index.ts
import { z } from "zod";
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";

export function registerMyCategoryTools(server: McpServer) {
  server.tool(
    "myNewTool", // unique name
    "Short description of what it does", // description
    {
      param1: z.string().describe("Example parameter"),
    },
    async ({ param1 }) => {
      // TOOL LOGIC ⤵️
      return {
        content: [{ type: "text", text: `You sent ${param1}` }],
      };
    }
  );
}
```

2. **Hook the category into the global registry**

Add (or update) the import in `src/tools/index.ts` and call the register function inside `registerAllTools`:

```typescript
// src/tools/index.ts
import { registerMyCategoryTools } from "./myCategory/index.js";

export function registerAllTools(server: McpServer) {
  // …existing categories
  registerMyCategoryTools(server);
}
```

That’s it – when the MCP server starts, every `registerXTools` function runs and your new tool becomes available immediately.

***

#### Testing Your Tools 🧪

1. Build the project after making changes:

```bash
npm run build
```

2. Link the package locally for testing:

```bash
npm link
```

3. Test the MCP server directly:

```bash
# Run the server directly
node build/src/index.js

# Or use the CLI serve command
npx arbitrum-mcp-tools serve
```

4. To test with an AI assistant, temporarily modify your platform's config to point to the local build:

```json
{
  "mcpServers": {
    "arbitrum": {
      "command": "node",
      "args": ["/path/to/your/arbitrum-mcp-tools/build/src/index.js"]
    }
  }
}
```

5. Restart the AI assistant and verify your tools are available.

### Contributing 🙌

Contributions are welcome! Please feel free to submit a Pull Request.

### License 📜

This project is licensed under the MIT License - see the LICENSE file for details.


# Network MCP Tools


# Account Analysis

Tools for analyzing accounts, balances, and tokens.

1. **`getAccountBalance`** - Get native token balance for an Arbitrum address

   \
   [Demo](https://drive.google.com/file/d/1YLbyv1P6wc_gr_ME0tc3C2qsiwgV2lQ5/view?usp=sharing)<br>

   * **Parameters:**

     * `address`: Ethereum address to check balance for
     * `blockTag`: The optional block number, hash, or tag (e.g., 'latest', 'pending', 'safe', 'finalized', 'earliest') to get the balance for. Defaults to 'latest' if unspecified.

2. **`getTokenBalances`** - Get ERC-20 token balances for an Arbitrum address, optionally filtered by a list of contract addresses.<br>

   [Demo](https://drive.google.com/file/d/1NpvcbkARdmUdlk3YER6kTdXNSSBUSu_K/view?usp=drive_link)<br>

   * **Parameters:**

     * `address`: The owner address or ENS name to get the token balances for
     * `contractAddresses`: Optional list of contract addresses to filter by

3. **`getNfts`** - Get NFTs owned by an address, with options for filtering, pagination, and ordering.<br>

   [Demo](https://drive.google.com/file/d/1MzSe-z5-y5PxfxZW8JkTiLmXyrN0fgXb/view?usp=drive_link)<br>

   * **Parameters:**
     * `owner`: The address of the owner
     * `options`: (Optional) Object containing:

       * `contractAddresses`: Optional list of contract addresses to filter by (Limit 45)
       * `omitMetadata`: Optional boolean to omit NFT metadata (default: false)
       * `excludeFilters`: Optional list of filters (SPAM, AIRDROPS) to exclude
       * `includeFilters`: Optional list of filters (SPAM, AIRDROPS) to include
       * `pageSize`: Max NFTs to return (API default 50, max 100)
       * `tokenUriTimeoutInMs`: Timeout for metadata fetch
       * `orderBy`: Order by 'TRANSFERTIME'
       * `pageKey`: Optional page key for pagination

4. **`getTransactionHistory`** - Get transaction history for an Arbitrum address, with options for filtering and pagination.<br>

   [Demo](https://drive.google.com/file/d/1iKemjo5NCJxAne4D_SvmpcTKIke3vch1/view?usp=drive_link)<br>

   * **Parameters:**
     * `address`: The address to check transactions for (used as fromAddress)
     * `options`: (Optional) Object containing:

       * `fromBlock`: Start block ("0x0" default)
       * `toBlock`: End block ("latest" default)
       * `toAddress`: Recipient filter
       * `contractAddresses`: Contract filter (ERC20/721/1155)
       * `excludeZeroValue`: Exclude zero value transfers (true default)
       * `order`: 'asc'/'desc' by block number ('asc' default)
       * `category`: Array of categories (EXTERNAL, INTERNAL, ERC20, ERC721, ERC1155, SPECIALNFT)
       * `maxCount`: Max results per page (50 default)
       * `withMetadata`: Include transfer metadata (false default)
       * `pageKey`: Optional page key for pagination

5. **`getNftMetadata`** - Get metadata for an NFT given its contract address and token ID, with options for caching and token type.<br>

   [Demo](https://drive.google.com/file/d/1D9j7H7jON9znxZMLaAecePpArCb4WmaR/view?usp=drive_link)<br>

   * **Parameters:**
     * `contractAddress`: NFT contract address
     * `tokenId`: Token ID
     * `options`: (Optional) Object containing:
       * `tokenType`: Specify token type (ERC721, ERC1155, UNKNOWN)
       * `tokenUriTimeoutInMs`: Timeout for metadata fetch
       * `refreshCache`: Refresh metadata before response (false default)

6. **`getAccountProtocols`** - Analyze which smart contracts (protocols) an address interacts with most frequently.<br>

   [Demo](https://drive.google.com/)<br>

   * **Parameters:**
     * `address`: The address to analyze for protocol interactions
     * `maxResults`: Maximum number of top interacted protocol addresses to return (optional, default: 10)

***


# Batch Operations

Tools for performing operations on multiple addresses.

1. **`getBatchBalances`** - Get balances for multiple addresses in single call<br>

   [Demo](https://drive.google.com/file/d/1xUcXFFN2hRe_-NFesMaz2SQGWbMPN-n2/view?usp=drive_link)<br>

   * **Parameters:**
     * `addresses`: Array of addresses to check
     * `tokenAddress`: ERC-20 token address (optional)<br>
2. **`multiAddressAnalysis`** - Compare token holdings and transactions across multiple addresses<br>

   [Demo](https://drive.google.com/file/d/1wWFXYB0eFdgMMJZdStNNcrxn-ugZbY0J/view?usp=drive_link)<br>

   * **Parameters:**
     * `addresses`: Array of addresses to analyze
     * `includeNfts`: Include NFTs in analysis (optional boolean)
     * `includeTransactions`: Include transactions in analysis (optional boolean)


# Chain Data

Tools for retrieving blockchain data.<br>

1. **`getBlockNumber`** - Get the latest block number on Arbitrum<br>

   [Demo](https://drive.google.com/file/d/1Z36gY_aGq2ANg-dQEzIv2Mvi0i4pYwBe/view?usp=drive_link)<br>

   * **Parameters:** (No parameters)<br>
2. **`getBlock`** - Get details of a block by number or hash<br>

   [Demo](https://drive.google.com/file/d/15SeehSlLWjZzv5uhz8QUgxsEqntrr730/view?usp=drive_link)<br>

   * **Parameters:**
     * `block`: Block number (as a string), block hash, or one of the following tags: 'latest', 'pending', 'earliest'<br>
3. **`getTransaction`** - Get details of a transaction by hash<br>

   [Demo](https://drive.google.com/file/d/1TlYmxvuk3LP2pOEl3JO5XCKDTlCk4UYx/view?usp=drive_link)<br>

   * **Parameters:**
     * `txHash`: Transaction hash<br>
4. **`getTransactionReceipt`** - Get the transaction receipt for a given transaction hash<br>

   [Demo](https://drive.google.com/file/d/1fmMY8yitWbWMAbcL9qqmNIYMAc8gb4Vx/view?usp=drive_link)<br>

   * **Parameters:**
     * `txHash`: Transaction hash<br>
5. **`getGasParameters`** - Get detailed Arbitrum gas price metrics<br>

   [Demo](https://drive.google.com/file/d/1wtR1tghOCFdnkoOydVHYYY1uhK2gny6F/view?usp=drive_link)<br>

   * **Parameters:** (No parameters)<br>
6. **`getGasPrice`** - Get the current gas price on Arbitrum<br>

   [Demo](https://drive.google.com/file/d/1gsjKL_4VBXhhQYaTrsRGjBLg1mLxU8K8/view?usp=drive_link)<br>

   * **Parameters:** (No parameters)


# Cross-Chain Operations

Tools for cross-chain operations.

1. **`getTransactionLogs`** - Fetch and decode transaction logs from L1 or L2 with automatic network detection. Recognizes 15+ common Arbitrum events including cross-chain messaging, token transfers, and bridge operations with emoji indicators and structured output.<br>

   [Demo](https://drive.google.com/file/d/1NEJEsM7pbR6KonY1b5GUDy136NNgRs7s/view?usp=drive_link)<br>

   * **Parameters:**
     * `txHash`: Transaction hash (0x-prefixed, 66 chars) that works on both L1 (Ethereum) and L2 (Arbitrum). Includes automatic fallback between networks and comprehensive event decoding.


# Contract Interaction

Tools for interacting with smart contracts.

1. **`getContractCode`** - Retrieve the bytecode of a contract at a specific address and optionally at a given block.<br>

   [Demo](https://drive.google.com/file/d/11bD07fdUAYug_CtEmAVBit2_VRhnfdzR/view?usp=drive_link)<br>

   * **Parameters:**
     * `contractAddress`: The address or ENS name of the account to get the code for
     * `blockTag`: The optional block number, hash, or tag (e.g., 'latest', 'pending', 'safe', 'finalized', 'earliest') to get the code for. Defaults to 'latest' if unspecified.<br>
2. **`decodeTransactionCalldata`** - Decode transaction input data using Arbitrum contract ABIs with comprehensive error handling and detailed output formatting. Automatically detects the target contract from transaction hash and provides intelligent troubleshooting guidance.<br>

   [Demo](https://drive.google.com/file/d/1dFpukRTkYY8RmqWyziSRqnzkomZClHlF/view?usp=drive_link)<br>

   * **Parameters:**
     * `transactionHash`: Transaction hash to decode (automatically detects contract address from transaction). Supports contract creation detection, invalid calldata handling, and provides detailed function parameter analysis with type information.<br>
3. **`getContractEvents`** - Query specific events from Arbitrum contracts with intelligent block range management and auto-discovery<br>

   [Demo](https://drive.google.com/file/d/1NfotfXWqvWLPrqedHSRlU04DGOmAJl-L/view?usp=drive_link)<br>

   * **Parameters:**
     * `contractAddress`: Contract address
     * `eventSignature`: Event signature (e.g., 'Transfer(address,address,uint256)') (optional)
     * `fromBlock`: Starting block number (optional)
     * `toBlock`: Ending block number (optional)
     * `maxBlocks`: Maximum blocks per query (default: 500)
     * `limit`: Maximum number of events to return (default: 1000)
     * `topics`: Additional topic filters (optional)
     * `autoDiscover`: Automatically find active periods if no events found (default: true)
     * `searchDepth`: Number of block ranges to search when auto-discovering (default: 5)<br>
4. **`getTokenAllowance`** - Get ERC-20 token allowance for an owner and spender<br>

   [Demo](https://drive.google.com/file/d/1BdndjrIOXLUpLF4hrRzdAsQy1OeCY0jH/view?usp=drive_link)<br>

   * **Parameters:**
     * `tokenAddress`: ERC-20 token contract address
     * `owner`: Owner address
     * `spender`: Spender address


# Development

Tools for development process.<br>

1. **`simulateTransaction`** - Simulate Arbitrum transaction with comprehensive asset change detection and detailed error analysis. Provides formatted output with gas usage, ETH transfers, and transaction impact assessment.<br>

   [Demo](https://drive.google.com/file/d/1Vh6IqShs3TCKzPtt3IEAnAG85ZdoNLGC/view?usp=drive_link)<br>

   * **Parameters:**
     * `from`: From address (0x-prefixed)
     * `to`: To address (0x-prefixed)
     * `data`: Optional transaction calldata (hex string)
     * `value`: Optional value in wei (hex string)
     * `gas`: Optional gas limit (hex string)
     * Includes automatic error detection and asset change analysis.<br>
2. **`estimateGas`** - Estimate gas usage for a transaction<br>

   [Demo](https://drive.google.com/file/d/12R-3EKbmiBkzfvaSuioFVmQlrtEXJFMV/view?usp=drive_link)<br>

   * **Parameters:**
     * `to`: Destination address
     * `from`: Optional sender address
     * `data`: Optional transaction data (hex string)
     * `value`: Optional value in wei as a string (e.g., '1000000000000000000')
     * `gasPrice`: Optional gas price in wei as a string (e.g., '20000000000')
     * `nonce`: Optional transaction nonce as a string (e.g., '0', '1')
     * `type`: Optional EIP-2718 transaction type (e.g., 0 for legacy, 2 for EIP-1559)


# Stylus MCP Tools

Tools for Stylus development and interaction.

1. **`createStylusProject`** - Create a new Cargo Stylus project<br>

   [Demo](https://drive.google.com/file/d/1L8C2_bERV9Qs-RCN1adj4_vALC6wP1Y_/view?usp=drive_link)<br>

   * **Parameters:**
     * `projectName`: Project name
     * `path`: Path to create the project (optional)<br>
2. **`initStylusProject`** - Initialize a Stylus project in the current directory<br>

   [Demo](https://drive.google.com/file/d/1OlD6eQ3oQ8EjI8rYe5VGpQj0ytwmIgeG/view?usp=drive_link)<br>

   * **Parameters:**
     * `path`: Path to initialize the project (optional)<br>
3. **`exportStylusAbi`** - Export a Solidity ABI for a Stylus contract<br>

   [Demo](https://drive.google.com/file/d/1BtK6XyFSBydpqo2DAG5vhDFxNnWKIQu3/view?usp=drive_link)<br>

   * **Parameters:**
     * `output`: The output file
     * `path`: Path to the Stylus project (optional)
     * `json`: Write a JSON ABI instead using solc. Requires solc (default: true)
     * `rustFeatures`: Rust crate's features list. Required to include feature specific ABI (optional)<br>
4. **`checkStylusContract`** - Check if a Stylus contract is valid for deployment

   \
   [Demo](https://drive.google.com/file/d/1_a83wu32IpPW2YqorbX9dAkhMb9qNt7T/view?usp=drive_link)<br>

   * **Parameters:**
     * `path`: Path to the Stylus project (optional)<br>
5. **`deployStylusContract`** - Deploy a Stylus contract to the Arbitrum network. Uses environment variables for secure authentication and supports gas estimation mode.<br>

   [Demo](https://drive.google.com/file/d/1JcHpcLmCaAiR0rcVMRKvfd2V-BGBvlVB/view?usp=drive_link)<br>

   * **Parameters:**
     * `endpoint`: RPC endpoint URL
     * `path`: Path to the Stylus project (optional)
     * `estimateGas`: Only estimate gas instead of deploying (optional boolean)
     * Uses STYLUS\_PRIVATE\_KEY, STYLUS\_PRIVATE\_KEY\_PATH, or STYLUS\_KEYSTORE\_PATH environment variables for authentication.<br>
6. **`verifyStylusContract`** - Verify the deployment of a Stylus contract<br>

   [Demo](https://drive.google.com/file/d/1ux1o4NOhQOYr0auNryTV_wFGjCUGlLse/view?usp=drive_link)<br>

   * **Parameters:**
     * `deploymentTx`: Deployment transaction hash
     * `endpoint`: RPC endpoint URL (optional)
     * `path`: Path to the Stylus project (optional)<br>
7. **`activateStylusContract`** - Activate an already deployed Stylus contract. Uses environment variables for secure authentication.<br>

   [Demo](https://drive.google.com/file/d/1JWDFVtSAgBCtcXg4NXJkhrTlKM-IXxTt/view?usp=drive_link)<br>

   * **Parameters:**
     * `contractAddress`: Deployed contract address
     * `endpoint`: RPC endpoint URL
     * `path`: Path to the Stylus project (optional)
     * Uses STYLUS\_PRIVATE\_KEY, STYLUS\_PRIVATE\_KEY\_PATH, or STYLUS\_KEYSTORE\_PATH environment variables for authentication.<br>
8. **`cacheStylusContract`** - Cache a contract using the Stylus CacheManager. Uses environment variables for secure authentication and supports multiple cache operations.<br>

   [Demo](https://drive.google.com/file/d/1ziUn3-j578S8TJxXUUSG8CySpxFpMsC0/view?usp=drive_link)<br>

   * **Parameters:**
     * `subcommand`: Cache subcommand ('bid', 'status', 'suggest-bid', 'help')
     * `contractAddress`: Contract address to cache
     * `endpoint`: RPC endpoint URL
     * `path`: Path to the Stylus project (optional)
     * `bidAmount`: Bid amount for 'bid' subcommand (optional)
     * Uses STYLUS\_PRIVATE\_KEY, STYLUS\_PRIVATE\_KEY\_PATH, or STYLUS\_KEYSTORE\_PATH environment variables.<br>
9. **`generateStylusBindings`** - Generate C code bindings for a Stylus contract from project source with automatic ABI preparation and cleanup<br>

   [Demo](https://drive.google.com/file/d/13DDM55sDEmHPqUm7EEjQSPs_S7_DDmLH/view?usp=drive_link)<br>

   * **Parameters:**
     * `projectPath`: The Stylus project path
     * `outDir`: Output directory for C bindings
     * `rustFeatures`: Rust features for ABI generation (optional)
     * `abiOutputPath`: Custom ABI JSON path (optional)
     * `keepAbiFile`: Keep generated ABI file (optional, default: false)<br>
10. **`replayStylusTransaction`** - Replay a Stylus transaction in GDB debugger<br>

    [Demo](https://drive.google.com/file/d/1e2Q-iUmVGjUJ0Vu_0HNxgCxZEB90qhVj/view?usp=drive_link)<br>

    * **Parameters:**
      * `txHash`: Transaction hash to replay
      * `endpoint`: RPC endpoint URL (optional)
      * `path`: Path to the Stylus project (optional)<br>
11. **`traceStylusTransaction`** - Trace a Stylus transaction<br>

    [Demo](https://drive.google.com/file/d/10Stad8Gi50IgUoJPmOK03IWdrB1MPhsV/view?usp=drive_link)<br>

    * **Parameters:**
      * `txHash`: Transaction hash to trace
      * `endpoint`: RPC endpoint URL (optional)
      * `path`: Path to the Stylus project (optional)<br>
12. **`deployMultipleStylusContracts`** - Deploy multiple Stylus contracts to the Arbitrum network in sequence<br>
    * **Parameters:**
      * `endpoint`: RPC endpoint URL
      * `projectPaths`: Array of paths to Stylus projects that should be deployed
      * `estimateGas`: Only estimate gas instead of deploying (optional boolean)
      * Uses `STYLUS_PRIVATE_KEY`, `STYLUS_PRIVATE_KEY_PATH`, or `STYLUS_KEYSTORE_PATH` environment variables for authentication.


