# Canonical factory contracts

Deploying new Arbitrum chains is usually done through a `RollupCreator` contract that processes the creation of the needed contracts and sends the initialization messages from the parent to the child chain. Similarly, creating a token bridge for an Arbitrum chain is usually done using a `TokenBridgeCreator` contract that creates the token bridge contracts in both the parent and child chains (this last one via [Parent-to-child messages](/how-arbitrum-works/deep-dives/l1-to-l2-messaging.mdx)).

This page describes the benefits of using these canonical factory contracts and lists their addresses in all supported chains.

:::info Use the Arbitrum Chain SDK

You can use these contracts to create Arbitrum chains. However, it is strongly recommended to go through the [Chain SDK](/launch-arbitrum-chain/arbitrum-chain-sdk-introduction.mdx) to interact with them. Doing so prevents misconfiguring parameters and using appropriate defaults for most of them.

:::

## Benefits of using the canonical factory contracts

The main benefits of using the canonical factory contracts are:

- **End-to-end deployment and initialization**: The canonical contracts will create all needed contracts, initialize them, and configure them with the parameters passed. Additionally, they will send the appropriate initialization messages to the chain's Inbox contract so the sequencer can process them upon starting. This process is done atomically in a single transaction, guaranteeing a successful chain or token bridge creation.
- **Gas efficiency**: The canonical contract design is to be gas efficient. Creating and initializing all contracts for a chain or token bridge is a gas-consuming process, so special care has been taken to fit everything into one transaction.
- **Updated with the latest features**: Whenever a new version is available for the contracts of an Arbitrum chain, the canonical factory contracts get updated, so new Rollups and token bridges are created using the updated version.

## Addresses of the canonical factory contracts

This table shows the addresses of the deployed and maintained canonical factory contracts.

| Network          | Chain id | `RollupCreator`                                                                 | `TokenBridgeCreator`                                                            |
| ---------------- | -------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Ethereum         | 1        |         |         |
| Arbitrum One     | 42161    |     |     |
| Arbitrum Nova    | 42170    |     |     |
| Base             | 8453     |      |      |
| Sepolia          | 11155111 |  |  |
| Arbitrum Sepolia | 421614   |    |    |
| Base Sepolia     | 84532    |     |     |

## How to deploy new factory contracts

This section describes the process of deploying a new `RollupCreator` and a new `TokenBridgeCreator` on a parent chain.

:::warning The use of non-canonical factory contracts is unsupported

This section describes the process of deploying new factory contracts. This can be useful when creating Arbitrum chains on a parent chain that doesn't have canonical factory contracts, or when modifying the core or token bridge contracts. However, keep in mind that using factory contracts different than the ones listed above (canonical) is not supported and might lead to unexpected issues.

:::

### Deploying a `RollupCreator`

To deploy the `RollupCreator` and the core contract templates, we'll use the [`nitro-contracts`](https://github.com/OffchainLabs/nitro-contracts) repository.

#### Step 1: Clone `nitro-contracts` repo and checkout the desired release

```shell
git clone https://github.com/OffchainLabs/nitro-contracts.git
cd nitro-contracts
git checkout vX.Y.Z
```

#### Step 2: Install the dependencies and build the contracts

```shell
yarn install
yarn build:all
```

#### Step 3: Create the `.env` file and set the desired env parameters

```shell
cp .env-sample .env
```

We can use the following parameters:

- `DEVNET_PRIVKEY` or `MAINNET_PRIVKEY`: The private key of the account that will deploy the contracts. Use one or the other depending on the type of network where the contracts will be deployed: testnet or mainnet. Will be used in the `hardhat.config.ts` file.
- `DISABLE_VERIFICATION`: Whether to disable verification of contracts in the block explorer or not.
- `ETHERSCAN_API_KEY`: The key to access the API of the block explorer used. Will be used in the `hardhat.config.ts` file.

#### Step 4: Check hardhat configuration

Now we can open the `hardhat.config.ts` file and verify that the network where the contracts are going to be deployed exists in the file. If it exists, we can verify that it's using the environment variables specified above. If it doesn't exist, we can add the network to the configuration file.

#### Step 5: Create a `config.ts` file and specify the right maxDataSize

```shell
cp scripts/config.ts.example scripts/config.ts
```

Then we can modify the constant `maxDataSize` to one of the following values:

- `117964` is the parent chain is Ethereum
- `104857` if the parent chain is a Layer 2 chain

#### Step 6: Run the deployment script

```shell
yarn deploy-factory --network parentChainNetwork
```

This last step will create the template contracts and the `RollupCreator` contract, and will show all addresses in the output. It will optionally try to verify the contracts if the configuration is present.

### Deploying a `TokenBridgeCreator`

To deploy the `TokenBridgeCreator` and the token bridge contract templates, we'll use the [token-bridge-contracts](https://github.com/OffchainLabs/token-bridge-contracts) repository.

#### Step 1: Clone `token-bridge-contracts` repo and checkout the desired release

```shell
git clone https://github.com/OffchainLabs/token-bridge-contracts.git
cd token-bridge-contracts
git checkout vX.Y.Z
```

#### Step 2: Install the dependencies and build the contracts

```shell
yarn install
yarn build
```

#### Step 3: Create the .env file and set the desired env parameters

```shell
cp .env-sample .env
```

We can use the following parameters:

- `BASECHAIN_RPC`: RPC of the parent chain
- `BASECHAIN_DEPLOYER_KEY`: Private key of the account that will be deploying the contracts
- `BASECHAIN_WETH`: Address of the WETH contract on the parent chain (should be the zero address for custom gas token chains)
- `GAS_LIMIT_FOR_L2_FACTORY_DEPLOYMENT`: The gas limit for deploying the child chain factory contracts. It is recommended to leave the default value `6000000`
- `ARBISCAN_API_KEY`: (Optional) The key to access the API of the block explorer used for verifying the contracts

#### Step 4: Run the deployment script

```shell
yarn deploy:token-bridge-creator
```

This step will create the template contracts and the `TokenBridgeCreator` contract, and will show all addresses in the output.