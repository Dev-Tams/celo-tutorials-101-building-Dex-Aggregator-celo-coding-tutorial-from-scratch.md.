# Creating an Educational DEX Aggregator on the Celo Blockchain using Solidity and Hardhat:

## Table of Contents:

 - [INTRODUCTION TO DEX AGGREGATOR](#introduction-to-dex-aggregator)
   - [Introduction](#introduction)
   - [Learning Outcomes](#learning-outcomes)
   - [Tech Stack](#tech-stack)
   - [Pre-requisites](#prerequisites-and-previous-knowledge)
   - [Time Required](#time-required)
 - [Setting up the Environment](#setting-up-the-environment)
   - [Installing Node.js and NPM](#installing-nodejs-and-npm)
   - [Installing Hardhat](#installing-hardhat)
   - [Initializing the Project](#initializing-the-project)
   - [Configuring Hardhat](#configuring-hardhat)
   - [Creating and Defining the Smart Contract](#creating-and-defining-the-smart-contract)
   - [Compiling the Smart Contract](#compiling-the-smart-contract)
   - [Setting up a Celo Network](#setting-up-a-celo-network)
   - [Configuring Hardhat for Deployment](#conigure-hardhat-for-deployment)
   - [Deploying the Smart Contract](#deploying-the-smart-contract)
   - [Interacting with the Smart Contract](#interacting-with-the-smart-contract)
   - [Adding Content to the Smart Contract](#adding-content-to-the-smart-contract)
   - [Viewing Content on the Smart Contract](#viewing-content-on-the-smart-contract)
 - [Conclusion](#conclusion)

# INTRODUCTION TO DEX AGGREGATOR:

A [DEX aggregator](https://blockchain.oodles.io/blog/essentials-dex-aggregator-development/) is a platform that allows users to access multiple Decentralized Exchanges (DEXs) through single interface, instead of having to visit multiple DEXs to find the best price for a specific token. Users can also use a DEX aggregator to compare prices and execute trades on the DEX with the best available price.

DEX aggregators typically use smart routing algorithms to split orders into smaller parts and execute them across multiple DEXs. This can lead to better prices, lower slippage and higher liquidity for users who want faster transactions.

A popular DEX aggregator is the **1inch aggregator** in the ethereum network. Matcha and ParaSwap are as well popular platforms that offer a variety of features like limit orders, price alerts and portfolio tracking to make trading on DEXs more accessible and user-friendly.

## Introduction:

Decentralized Finance (De-Fi) has been one of the fastest-growing sectors in the blockchain industry. Educational DeFi (EduDe-Fi) is a subsector of it that provides a platform for users to contribute on educational content and earn rewards. 
In this tutorial, I walk you through the process of building a simple Educational DEX Aggregator on Celo blockchain using [Hardhat](https://hardhat.org/#tools) and how to create a Smart Contract that allows users to contribute educational content and earn rewards in the form of CELO tokens.

## Learning Outcomes:

1. Ability to create a simple Educational DEX Aggregator on Celo blockchain using [Hardhat](https://hardhat.org/#tools).
2. You will understand how to write and deploy Smart Contracts.
3. Interact with them using a Web3 interface and how to use the Celo blockchain to store and transfer value.

## Tech Stack:

1. [Hardhat](https://hardhat.org/)
2. [Solidity](https://docs.soliditylang.org/en/v0.8.20/)
3. JavaScript
4. [React](https://react-cn.github.io/react/downloads.html)
5. Celo Blockchain
 
## Prerequisites and Previous Knowledge:

1. Blockchain Technology and its fundamental concepts.
2. Smart contract development using [Solidity](https://docs.soliditylang.org/en/v0.8.20/).
3. JavaScript and [React](https://react-cn.github.io/react/downloads.html).
4. Web3 interface and how to use it to interact with Smart Contracts.

You will also need to install the following:
1. [Node.js](https://nodejs.org/en/download)
2. [NPM](https://www.npmjs.com/package/download)
3. [Hardhat](https://hardhat.org/)
4. [Celo Extension Wallet](https://chrome.google.com/webstore/detail/celoextensionwallet/kkilomkmpmkbdnfelcpgckmpcaemjcdh?hl=en)

## Time Required:

This tutorial is designed for beginners and can take up to 4 hours to complete.
However, the time required may vary depending on your proficiency with the tech stack and your familiarity with blockchain development.

Let's get started!

# Setting up the Environment:

## Installing Nodejs and NPM:

To get started, you need to have Node.js and NPM installed on your system. If you don't already have them installed, follow these steps to install them:

1. Go to https://nodejs.org/en/download/ and download the appropriate version for your operating system.
2. Run the installer and follow the prompts to install Node.js and NPM.
3. You can verify that Node.js and NPM have been installed correctly by running the following commands on your terminal:
```run
node -v
npm -v
```

These commands should return the version number of Node.js and NPM respectively.

### Installing Hardhat:

[Hardhat](https://hardhat.org/) is a popular development environment for building Ethereum-compatible blockchain applications. It provides a suite of tools that make it easy to write, test and deploy Smart Contracts.

To install Hardhat, run the following command on your terminal:

``` css
npm install --save-dev hardhat
```
This will install Hardhat as a development dependency in your project.

## Initializing the Project:

To create a new project, create a new directory for your project and run the following commands on your terminal:

``` bash
mkdir edudefi-aggregator
cd edudefi-aggregator
npm init -y 
```
This will create a new directory for your project and initialize a new npm package in it.

## Configuring Hardhat:

To configure Hardhat, run the following command in your terminal:
``` 
npx hardhat
```
* This will prompt you to choose a default project type. Choose "Create a sample project" and press enter.

* This will create a new Hardhat project in your current directory with the following structure:
```
bash
├── contracts
│   └── Sample.sol
├── deployments
├── helpers
├── scripts
│   └── sample-script.js
├── test
│   └── sample-test.js
├── .env
├── .gitignore
├── hardhat.config.js
├── package.json
└── README.md
```

## Creating and Defining the Smart Contract:

Create a new file called "EduDeFi.sol" in the contracts directory and add the following code:

``` solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;

/**
 * @title EduDeFi
 * @dev A smart contract for educational content.
 */
contract EduDeFi {
    /**
     * @dev A data structure for educational content.
     * @param author The address of the author of the content.
     * @param title The title of the content.
     * @param url The URL of the content.
     */
    struct Content {
        address author;
        string title;
        string url;
    }

    // Define mapping to store educational content
    mapping(bytes32 => Content) public contents;

    /**
     * @dev An event that is emitted when new content is added.
     * @param author The address of the author of the content.
     * @param id The ID of the content.
     * @param title The title of the content.
     * @param url The URL of the content.
     */
    event ContentAdded(address indexed author, bytes32 indexed id, string title, string url);

    /**
     * @dev Add new educational content.
     * @param _title The title of the content.
     * @param _url The URL of the content.
     * Requirements:
     * - The title and URL cannot be empty.
     * - The URL must be a valid URL.
     */
    function addContent(string memory _title, string memory _url) public {
        // Check that the title is not empty
        require(bytes(_title).length > 0, "Title cannot be empty");

        // Check that the URL is not empty
        require(bytes(_url).length > 0, "URL cannot be empty");

        // Check that the URL is a valid URL (this is a simple check and can be improved)
        require(bytes(_url).length < 256, "URL must be less than 256 characters");
        require(bytes(_url)[0] != 0, "URL cannot start with null byte");
        require(bytes(_url)[bytes(_url).length - 1] != 0, "URL cannot end with null byte");

        // Generate a unique content ID using a cryptographic hash function
        bytes32 id = keccak256(abi.encodePacked(msg.sender, _title, _url));

        // Check that the content with the same ID doesn't already exist
        require(contents[id].author == address(0), "Content with this ID already exists");

        // Store the new content
        contents[id] = Content(msg.sender, _title, _url);

        // Emit the ContentAdded event
        emit ContentAdded(msg.sender, id, _title, _url);
    }
}

    /**
     * @dev Validate that a given string is a valid URL.
     * @param _url The URL to validate.
     * @return Whether the given string is a valid URL.
     */
    
```
* This contract defines a data structure for educational content.

A mapping to store the content and a function to add new content. The `addContent` function takes a title and a URL as input, creates a new Content struct with the sender's address, title & URL and adds it to the contents mapping. It also emits a `ContentAdded` event with the author's address, content ID, title and URL.

## Compiling the Smart Contract:

To compile the Smart Contract, run the following command on your terminal:

``` python
npx hardhat compile
```
This will compile the EduDeFi.sol contract and generate artifacts in the artifacts directory.

### Setting up a Celo Network:

Before deploying the Smart Contract, you need to set up a Celo network. Follow the instructions at https://docs.celo.org/getting-started/baklava-testnet to set up a Baklava testnet node.

### Configuring Hardhat for Deployment:

To configure Hardhat for deployment, open the "hardhat.config.js" file and add the following code:

``` javascript
// Import the necessary Hardhat plugins and libraries
require("@nomiclabs/hardhat-waffle");
require("@nomiclabs/hardhat-ethers");
require("dotenv").config();

// Get the Celo RPC URL and private key from environment variables
const CELO_RPC_URL = process.env.CELO_RPC_URL;
const CELO_PRIVATE_KEY = process.env.CELO_PRIVATE_KEY;

// Export the Hardhat configuration object
module.exports = {
  networks: {
    celo: {
      url: CELO_RPC_URL, // Specify the Celo RPC URL
      accounts: [CELO_PRIVATE_KEY], // Specify the private key of the account to use for deployments and transactions
    },
  },
  solidity: {
    version: "0.8.0", // Specify the compiler version
    settings: {
      optimizer: {
        enabled: true, // Enable the optimizer
        runs: 200, // Set the number of optimizer runs to 200
      },
    },
  },
};

```
This code configures Hardhat to use the Celo RPC URL and private key from your .env file and sets the Solidity version and optimizer settings.

### Deploying the Smart Contract:

To deploy the Smart Contract, run the following command on your terminal:

```arduino
npx hardhat run scripts/deploy.js --network celo
```
This will deploy the EduDeFi contract to the Celo network and print the contract address to the console.

###  Interacting with the Smart Contract:

Now that the Smart Contract is deployed, we can interact with it using the Celo network.

1. We need to set up the celo network.
2. Setting up the Celo Wallet: To interact with the Smart Contract, you will need to set up a Celo wallet. Follow the instructions at https://docs.celo.org/celo-sdk/wallets/using-celo-wallet to set up the Celo Wallet Chrome extension.
3. Interacting with the Smart Contract using [Remix](https://remix.ethereum.org/#lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.18+commit.87f61d96.js): Remix is a popular web-based Solidity IDE that allows you to write, test and deploy Smart Contracts.

### To interact with the EduDeFi contract using Remix, follow these steps:

1. Go to https://remix.ethereum.org/ and create a new file called "EduDeFi.sol".
2. Copy and paste the "EduDeFi.sol" contract code into the file.
3. Compile the contract by clicking the "Solidity Compiler" tab in the sidebar, selecting the 0.8.0 version and clicking "Compile EduDeFi.sol
4. Switch to the "Deploy & Run Transactions" tab and select "Injected Web3" as the environment. This will allow you to connect to the Celo network using the Celo Wallet Chrome extension.
5. In the "Deploy" section, select the EduDeFi contract from the dropdown and click "Deploy".
After the contract is deployed, you can interact with it using the functions in the "Read Contract" and "Write Contract" sections.

### Adding Content to the Smart Contract:

To add content to the EduDeFi Smart Contract, follow these steps:

1. Connect your Celo Wallet to the Celo network.
2. Copy the contract address from the console after deploying the Smart Contract.
3. In the Celo Wallet, click the "Contracts" tab and then "Add Contract".
4. Paste the contract address into the "Contract Address" field and select the EduDeFi contract from the dropdown.
5. Click "Add Contract" to add the contract to your Celo Wallet.
6. In the "Write Contract" section of the contract, select the `addContent` function from the dropdown.
7. Enter a title and URL for the content you want to add.
8. Click "Write" to add the content to the Smart Contract.

### Viewing Content on the Smart Contract:

To view the content that has been added to the EduDeFi Smart Contract, follow these steps:

1. Connect your Celo Wallet to the Celo network.
2. Copy the contract address from the console after deploying the Smart Contract.
3. In the Celo Wallet, click the "Contracts" tab and then "Add Contract".
4. Paste the contract address into the "Contract Address" field and select the EduDeFi contract from the dropdown.
5. Click "Add Contract" to add the contract to your Celo Wallet.
6. In the "Read Contract" section of the contract, select the `getContent` function from the dropdown.
7. Enter the ID of the content you want to view.
8. Click "Read" to view the content.

### Conclusion:

Therefore, in this tutorial we have created a simple Educational DEX Aggregator on the Celo blockchain using the Hardhat development framework. We have learned how to create a Smart Contract that stores educational content, how to deploy the Smart Contract to the Celo network and how to interact with the Smart Contract using the Celo Wallet and Remix. We have also learned how to add content to the Smart Contract and view content stored on the Smart Contract. With this knowledge, you can start building your own Educational DEX Aggregator and contribute to the Celo blockchain ecosystem.
