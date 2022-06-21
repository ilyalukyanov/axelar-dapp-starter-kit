# Axelar cross-chain dApp starter kit

## Introduction

This repo provides a basic template to quickly bootstrap your application using the [Axelar Local Development Environment](https://github.com/axelarnetwork/axelar-local-dev), which simulates the relay of messages cross-chain, on the backend.

The code provides a basic scaffold for:

-   Solidity contract templates (`contract_templates` directory)
-   a web interface (`web` directory)

Once ready, you can use this repo to deploy your contracts to testnet.

## One-time setup

Install [nodejs](https://nodejs.org/en/download/). Run `node -v` to check your installation.

Clone this repo:

```bash
git clone https://github.com/axelarnetwork/axelar-dapp-starter-kit.git
```

Install dependencies:

```bash
npm update && npm install
```

## Build

1. In order to run your application against the local emulator, cd to the root directory of this project and run the command below. NOTE: Leave this node running on a separate terminal before deploying and testing the dApps.

```bash
npm run run-local-env
```

2. Build and deploy your application locally.

First, set up a `.env` file based on the `.env.sample` template in the root directory and update your local wallet for testing. Use either EVM_MNEMONIC or EVM_PRIVATE_KEY, but not both!

Then run the following command:

```bash
npm run build
npm run deploy <TEMPLATE_DIRECTORY> <ENVIRONMENT>
```

e.g. `npm run deploy CallContractWithToken local`

This will build your contracts in the `build` folder and the `web` directory for the UI build.

-   `info` for contract addresses by environment
-   `web/abi` for relevant ABIs, abd `web/info` for the network info for the UI

3. Test, either through the command line via script or (optionally) through this built-in UI

Option 1: Via command line:

a. The `index.js` file already has the base scaffold for how to invoke you new contract. Update that file to tailor to your code implementation
b. Then run `npm run invoke-contract <TEMPLATE_DIRECTORY> <ENVIRONMENT> <SRC_CHAIN> <DEST_CHAIN> <AMOUNT> <ADDR_1> <ADDR_2> <OTHER_ADDRESSES>` (with your custom args as needed)
e.g. `npm run invoke-contract CallContractWithToken local Ethereum Avalanche 40 0x74Ccd7d9F1F40417C6F7fD1151429a2c44c34e6d 0x3B94CbD6d0f09db75435d6E3c9449a6B70BB55E2`

Option 2: run your UI in the following steps:

a. In a separate terminal window, cd to the `web` directory
b. Set up a `.env.local` file based on the `.env.sample` template in the `web` directory and update either a NEXT_PUBLIC_EVM_MNEMONIC or NEXT_PUBLIC_EVM_PRIVATE_KEY (but not both) used for testing.
c. run `npm install`
d. run `npm run dev`
e. check out `http://localhost:3000` in the browser
f. enter params in the UI. in the text input, be sure to hit the "Enter" key after each destination address!

5. Once you are comfortable with your local dev scripts, deploying it to testnet should be simple:

```bash
npm run deploy <TEMPLATE_DIRECTORY> testnet
```

e.g. `npm run deploy CallContractWithToken testnet`

Ensure that the account tied to your EVM_MNEMONIC has enough funds to deploy to all supported EVM chains!
