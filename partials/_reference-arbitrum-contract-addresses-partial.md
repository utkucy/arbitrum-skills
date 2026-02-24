# Arbitrum Contract Addresses Reference

The following information may be useful to those building on Arbitrum. We list the addresses of the smart contracts related to the protocol, the token bridge and precompiles of the different Arbitrum chains.

## Protocol smart contracts

### Core contracts

The following contracts are deployed on Ethereum (L1)

|                 | Arbitrum One                                                                                   | Arbitrum Nova                                                                                  | Arbitrum Sepolia                                                                                      |
| --------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Rollup          |  |  |  |
| Sequencer Inbox |  |  |  |
| CoreProxyAdmin  |  |  |  |

### Cross-chain messaging contracts

The following contracts are deployed on Ethereum (L1)

|                      | Arbitrum One                                                                                                                                                                                         | Arbitrum Nova                                                                                  | Arbitrum Sepolia                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Delayed Inbox        |                                                                                                        |  |  |
| Bridge               |                                                                                                        |  |  |
| Outbox               |                                                                                                        |  |  |
| Classic Outbox\*\*\* |  <br />  |                                                                                                |                                                                                                       |

\*\*\*Migrated Network Only

### Fraud proof contracts

The following contracts are deployed on Ethereum (L1)

|                     | Arbitrum One                                                                                   | Arbitrum Nova                                                                                  | Arbitrum Sepolia                                                                                      |
| ------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| ChallengeManager    |  |  |  |
| OneStepProver0      |  |  |  |
| OneStepProverMemory |  |  |  |
| OneStepProverMath   |  |  |  |
| OneStepProverHostIo |  |  |  |
| OneStepProofEntry   |  |  |  |

## Token bridge smart contracts

### Core contracts

The following contracts are deployed on Ethereum (L1)

|                       | Arbitrum One                                                                                   | Arbitrum Nova                                                                                  | Arbitrum Sepolia                                                                                      |
| --------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| L1 Gateway Router     |  |  |  |
| L1 ERC20 Gateway      |  |  |  |
| L1 Arb-Custom Gateway |  |  |  |
| L1 Weth Gateway       |  |  |  |
| L1 Weth               |  |  |  |
| L1 Proxy Admin        |  |  |  |

The following contracts are deployed on the corresponding L2 chain

|                       | Arbitrum One                                                                                       | Arbitrum Nova                                                                                      | Arbitrum Sepolia                                                                                    |
| --------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| L2 Gateway Router     |  |  |  |
| L2 ERC20 Gateway      |  |  |  |
| L2 Arb-Custom Gateway |  |  |  |
| L2 Weth Gateway       |  |  |  |
| L2 Weth               |  |  |  |
| L2 Proxy Admin        |  |  |  |

## Precompiles

The following precompiles are deployed on every L2 chain and always have the same address

|                  | Arbitrum One                                                                                       | Arbitrum Nova                                                                                      | Arbitrum Sepolia                                                                                    |
| ---------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ArbAddressTable  |  |  |  |
| ArbAggregator    |  |  |  |
| ArbFunctionTable |  |  |  |
| ArbGasInfo       |  |  |  |
| ArbInfo          |  |  |  |
| ArbOwner         |  |  |  |
| ArbOwnerPublic   |  |  |  |
| ArbRetryableTx   |  |  |  |
| ArbStatistics    |  |  |  |
| ArbSys           |  |  |  |
| ArbWasm          |  |  |  |
| ArbWasmCache     |  |  |  |
| NodeInterface    |  |  |  |

## Misc

The following contracts are deployed on the corresponding L2 chain

| Function                    | Arbitrum One                                                                                       | Arbitrum Nova                                                                                      | Arbitrum Sepolia                                                                                    |
| --------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| L2 Multicall                |  |  |  |
| `ResourceConstraintManager` |  |  |