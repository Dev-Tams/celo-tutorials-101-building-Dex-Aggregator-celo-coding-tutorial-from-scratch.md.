# Creating an Educational DEx Aggregator on the Celo Blockchain with Solidity and Hardhat.md

## Table of Content

 - [INTRODUCTION](#introduction-to-dex-aggregator)
   - [introduction](#introduction)
   - [Learning Objectives](#learning-objectives)
   - [Tech Stack](#tech-stack)
   - [Prerequisites and Previous Knowledge](#prerequisites-and-previous-knowledge)
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

 A tutorial based on how to create a dex on celo blockchain.
 
 # INTRODUCTION TO DEX AGGREGATOR
 A DEX aggregator is a platform that allows users to access multiple decentralized exchanges (DEXs) through a single interface, Instead of having to visit multiple DEXs to find the best price for a specific token, users can use a DEX aggregator to compare prices and execute trades on the DEX with the best available price.

DEX aggregators typically use smart routing algorithms to split orders into smaller parts and execute them across multiple DEXs. This can lead to better prices, lower slippage, and higher liquidity for users with fast transactions.

a popular DEX aggregator is the 1inch aggregator in the ethereum network. Matcha, and ParaSwap are as well popular platforms that offer a variety of features such as limit orders, price alerts, and portfolio tracking to make trading on DEXs more accessible and user-friendly.

## Introduction:
Decentralized finance (DeFi) has been one of the fastest-growing sectors in the blockchain industry. Educational DeFi (EduDeFi) is a subsector that provides a platform for users to contribute educational content and earn rewards. 
In this tutorial, I walk you through the process of building a simple Educational DEX Aggregator on Celo blockchain using Hardhat. taking to note how to create a smart contract that allows users to contribute educational content and earn rewards in the form of CELO tokens.

## Learning Objectives
Objective:
~Ability to create a simple Educational DEX Aggregator on Celo blockchain using Hardhat.
~You will understand how to write and deploy smart contracts.
~Interact with them using a web3 interface, and how to use the Celo blockchain to store and transfer value.

## Tech Stack:
stacks required to scale through the tutorial
* Hardhat
* Solidity
* JavaScript
* React
* Celo Blockchain
 
## Prerequisites and Previous Knowledge:
To follow along with this tutorial, you should have basic knowledge of:

* Blockchain and its fundamental concepts
* Smart contract development using Solidity
* JavaScript and React
* Web3 interface and how to use it to interact with smart contracts

You will also need to install:
* Node.js
* NPM
* Hardhat

### Time Required:
This tutorial is designed for beginners and can take up to 4 hours to complete.
However, the time required may vary depending on your proficiency with the tech stack and your familiarity with blockchain development, most importantly if you dont get attack by bugs, lol


Let's get started!

# Setting up the Environment
### Installing Node.js and NPM
### Installing Hardhat

### Installing Nodejs and NPM
To get started, you need to have Node.js and NPM installed on your system. If you don't already have them installed, follow these steps to install them:

Go to https://nodejs.org/en/download/ and download the appropriate version for your operating system.
Run the installer and follow the prompts to install Node.js and NPM.
You can verify that Node.js and NPM have been installed correctly by running the following commands in your terminal:

run
		node -v
		npm -v


These commands should return the version number of Node.js and NPM respectively.

### Installing Hardhat
Hardhat is a popular development environment for building Ethereum-compatible blockchain applications. It provides a suite of tools that make it easy to write, test, and deploy smart contracts.

To install Hardhat, run the following command in your terminal:

``` css
npm install --save-dev hardhat
```

This will install Hardhat as a development dependency in your project.

*  Creating the Project
*  Initializing the Project
*  Configuring Hardhat

## Initializing the Project
To create a new project, create a new directory for your project and run the following commands in your terminal:

``` bash
mkdir edudefi-aggregator
cd edudefi-aggregator
npm init -y 
```

This will create a new directory for your project and initialize a new npm package in it.

## Configuring Hardhat
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

### In the next step, we will create a new Solidity contract in the contracts directory.

* Creating and Defining the Smart Contract
* Compiling the Smart Contract

### Creating and Defining the Smart Contract
Create a new file called EduDeFi.sol in the contracts directory and add the following code:
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
    mapping(uint256 => Content) public contents;
    uint256 public contentCount;

    /**
     * @dev An event that is emitted when new content is added.
     * @param author The address of the author of the content.
     * @param id The ID of the content.
     * @param title The title of the content.
     * @param url The URL of the content.
     */
    event ContentAdded(address indexed author, uint256 indexed id, string title, string url);

    /**
     * @dev Add new educational content.
     * @param _title The title of the content.
     * @param _url The URL of the content.
     * Requirements:
     * - The title and URL cannot be empty.
     * - The URL must be a valid URL, starting with "http://" or "https://".
     */
    function addContent(string memory _title, string memory _url) public {
        require(bytes(_title).length > 0, "Title cannot be empty");
        require(bytes(_url).length > 0, "URL cannot be empty");

        // Ensure that the URL is valid by checking that it starts with "http://" or "https://"
        require(bytes(_url).length >= 7, "Invalid URL");
        require(bytes(_url)[0] == "h" && bytes(_url)[1] == "t" && bytes(_url)[2] == "t" && bytes(_url)[3] == "p" && bytes(_url)[4] == "s" && bytes(_url)[5] == ":", "Invalid URL");
        contents[contentCount] = Content(msg.sender, _title, _url);
        contentCount++;

        emit ContentAdded(msg.sender, contentCount - 1, _title, _url);
    }
}
```
* This contract defines a data structure for educational content
a mapping to store the content, and a function to add new content. The addContent function takes a title and a URL as input, creates a new Content struct with the sender's address, title, and URL, and adds it to the contents mapping. It also emits a ContentAdded event with the author's address, content ID, title, and URL.

### Compiling the Smart Contract
To compile the smart contract, run the following command in your terminal:
``` python
npx hardhat compile
```

### This will compile the EduDeFi.sol contract and generate artifacts in the artifacts directory.

* Deploying the Smart Contract
* Setting up a Celo Network
* Configuring Hardhat for Deployment
* Deploying the Smart Contract

### Setting up a Celo Network
Before deploying the smart contract, you need to set up a Celo network. Follow the instructions at https://docs.celo.org/getting-started/baklava-testnet to set up a Baklava testnet node.

### Configuring Hardhat for Deployment
To configure Hardhat for deployment, open the hardhat.config.js file and add the following code:
``` javascript
require("@nomiclabs/hardhat-waffle");
require("@nomiclabs/hardhat-ethers");
require("dotenv").config();

const CELO_RPC_URL = process.env.CELO_RPC_URL;
const CELO_PRIVATE_KEY = process.env.CELO_PRIVATE_KEY;

module.exports = {
  networks: {
    celo: {
      url: CELO_RPC_URL,
      accounts: [CELO_PRIVATE_KEY],
    },
  },
  solidity: {
    version: "0.8.0",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200,
      },
    },
  },
};
```
This code configures Hardhat to use the Celo RPC URL and private key from your .env file, and sets the Solidity version and optimizer settings.

### Deploying the Smart Contract
To deploy the smart contract, run the following command in your terminal:

```arduino
npx hardhat run scripts/deploy.js --network celo
```
This will deploy the EduDeFi contract to the Celo network and print the contract address to the console.

###  Interacting with the Smart Contract
Now that the smart contract is deployed, we can interact with it using the Celo network.
firstly we need to set up the celo network.

* .2 Setting up the Celo Wallet
To interact with the smart contract, you will need to set up a Celo wallet. Follow the instructions at https://docs.celo.org/celo-sdk/wallets/using-celo-wallet to set up the Celo Wallet Chrome extension.

* .3 Interacting with the Smart Contract using Remix
Remix is a popular web-based Solidity IDE that allows you to write, test, and deploy smart contracts.

### To interact with the EduDeFi contract using Remix, follow these steps:

* Go to https://remix.ethereum.org/ and create a new file called EduDeFi.sol.
* Copy and paste the EduDeFi.sol contract code into the file.
* Compile the contract by clicking the "Solidity Compiler" tab in the sidebar, selecting the 0.8.0 version, and clicking "Compile EduDeFi.sol

* Switch to the "Deploy & Run Transactions" tab and select "Injected Web3" as the environment. This will allow you to connect to the Celo network using the Celo Wallet Chrome extension.
* In the "Deploy" section, select the EduDeFi contract from the dropdown and click "Deploy".
After the contract is deployed, you can interact with it using the functions in the "Read Contract" and "Write Contract" sections.

### Adding Content to the Smart Contract
To add content to the EduDeFi smart contract, follow these steps:

* Connect your Celo Wallet to the Celo network.
* Copy the contract address from the console after deploying the smart contract.
* In the Celo Wallet, click the "Contracts" tab and then "Add Contract".
* Paste the contract address into the "Contract Address" field and select the EduDeFi contract from the dropdown.
* Click "Add Contract" to add the contract to your Celo Wallet.
* In the "Write Contract" section of the contract, select the addContent function from the dropdown.
* Enter a title and URL for the content you want to add.
* Click "Write" to add the content to the smart contract.

### Viewing Content on the Smart Contract
To view the content that has been added to the EduDeFi smart contract, follow these steps:

* Connect your Celo Wallet to the Celo network.
* Copy the contract address from the console after deploying the smart contract.
* In the Celo Wallet, click the "Contracts" tab and then "Add Contract".
* Paste the contract address into the "Contract Address" field and select the EduDeFi contract from the dropdown.
* Click "Add Contract" to add the contract to your Celo Wallet.
* In the "Read Contract" section of the contract, select the getContent function from the dropdown.
* Enter the ID of the content you want to view.
* Click "Read" to view the content.

### Conclusion
In this tutorial, we have created a simple educational dex aggregator on the Celo blockchain using the Hardhat development framework. We have learned how to create a smart contract that stores educational content, how to deploy the smart contract to the Celo network, and how to interact with the smart contract using the Celo Wallet and Remix. We have also learned how to add content to the smart contract and view content stored on the smart contract. With this knowledge, you can start building your own educational dex aggregator and contribute to the Celo blockchain ecosystem.
