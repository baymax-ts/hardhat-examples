# hardhat-reef-examples

hardhat-reef-examples shows the use of [hardhat-reef](https://github.com/reef-chain/hardhat-plugin-reef) plugin to interact with the Reef chain.


## Installing

Install dependencies with `yarn`.


## Running

Define your Reef chain URL in `hardhat.config.js` (by default `ws://127.0.0.1:9944`):

```
module.exports = {
  solidity: "0.7.3",
  defaultNetwork: "reef",
  networks: {
    reef: {
      url: "ws://127.0.0.1:9944",
    },
    reef_testnet: {
      url: "wss://rpc-testnet.reefscan.com/ws",
      scanUrl: "https://api-testnet.reefscan.com", 
      seeds: {
        testnet_account: "<MNEMONIC_SEED>",
      },
    },
    reef_mainnet: {
      url: "wss://rpc.reefscan.com/ws",
      scanUrl: "wss://api.reefscan.com",
      seeds: {
        mainnet_account: "<MNEMONIC_SEED>",
      },
    },
  },
};
```

Copy `.env.example` to `.env` (`cp .env.example .env`) and update the desired mnemonic variable to your account seed mnemonic for the corresponding network.

You can have multiple accounts by listing them in dictionary with your custom name:

```
seeds: {
	account1: "<MNEMONIC_SEED1>",
	account2: "<MNEMONIC_SEED2>",
	...
},
```

In JS script you can select the account with:
```
const reef = await hre.reef.getSignerByName("account1");
```
where `account1` is the key of the item in the `seeds` dictionary.

If you get the following error:
```
Invalid Transaction: Inability to pay some fees , e.g. account balance too low
```

it is most likely because the accounts defined in the `hardhat.config.js` and JS script do not match.


## Scripts

See `scripts/` folder for example scripts, e.g. to deploy flipper run:

```
yarn hardhat run scripts/flipper/deploy.js 
```

After the contract is deployed, you can interact with it using the `flip.js` script:

```
yarn hardhat run scripts/flipper/flip.js 
```

make sure the `flipperAddress` corresponds to the deployed address.

Deploy and verify Token contract:
```
yarn hardhat run scripts/erc20/deploy_and_verify.js --network reef_testnet
```

## Integration localhost tests with reef-explorer

```
yarn hardhat run scripts/integration-test.js
```

## Deploying on testnet
The above commands will deploy on development (local) network by default. To deploy on testnet, use the `--network` flag:

```
yarn hardhat run scripts/flipper/deploy.js --network reef_testnet 
```

To get initial REEF tokens on the testnet, visit [Reef Discord testnet-faucet](https://discord.com/channels/793946260171259904/1087737503550816396) 
