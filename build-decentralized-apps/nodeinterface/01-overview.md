# NodeInterface overview

The Arbitrum Nitro software includes a special `NodeInterface` contract available at address `0xc8` that is only accessible via RPCs (it's not actually deployed onchain and thus can't be called by smart contracts). The way it works is that the node uses Geth's [`InterceptRPCMessage`](https://github.com/OffchainLabs/go-ethereum/blob/@@goEthereumCommit=6b19938827e8d7684caf6a883765d51ee967f250@@/internal/ethapi/api.go#L1034) hook to detect messages sent to the address `0xc8`, and swaps out the message it's handling before deriving a transaction from it.

The [reference page](/build-decentralized-apps/nodeinterface/02-reference.mdx) contains information about all methods available in the `NodeInterface`.