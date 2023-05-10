# Creating an Educational DEX Aggregator on the Celo Blockchain with Solidity and Hardhat

A tutorial based on how to create a DAO on celo blockchain.
<br/>

A DEX aggregator is a platform that allows users to access multiple decentralized exchanges (DEXs) through a single interface, Instead of having to visit multiple DEXs to find the best price for a specific token, users can use a DEX aggregator to compare prices and execute trades on the DEX with the best available price.

DEX aggregators typically use smart routing algorithms to split orders into smaller parts and execute them across multiple DEXs. This can lead to better prices, lower slippage, and higher liquidity for users with fast transactions.
<br/>

A popular DEX aggregator is the 1inch aggregator in the ethereum network. Matcha, and ParaSwap are as well popular platforms that offer a variety of features such as limit orders, price alerts, and portfolio tracking to make trading on DEXs more accessible and user-friendly.

## Table of Contents

- [Creating an Educational DEX Aggregator on the Celo Blockchain with Solidity and Hardhat
](#Creating-an-Educational-DEX-Aggregator-on-the-Celo-Blockchain-with-Solidity-and-Hardhat)
  - [1.1 Introduction](#introduction)
  - [Table of Contents](#table-of-contents)
  - [Learning Objective](#Learning-objective)
  - [Tech Stack](#Tech-Stack)
  - [Prerequisites and Previous Knowledge](#Prerequisites-and-Previous-Knowledge)
  - [Time Required](#Time-Required)
  - [Tutorial](#tutorial)
    - [Setting up the Environment](#Setting-up-the-Environment)
       - [Installing Node.js and NPM](#Installing-Node.js-and-NPM)
       - [Installing Hardhat](#Installing HardhaT)
    - [Step 2 - Install the necessary dependencies](#Step-2-Install-the-necessary-dependencies)
    - [Step 3 - Set up your .env file](#Step-3-Set-up-your-env-file)
    - [Step 4 - Write your Educational DAO contract](#Step-4-Write-your-Educational-DAO-contract)
    - [Step 5 - Write a Hardhat test script](#Step-5-Write-a-Hardhat-test-script)
    - [Step 6 - Deploy the contract](#Step-6-Deploy-the-contract)
    - [Step 7 - Interact with the contract](#Step-7-Interact-with-the-contract)
    - [Conclusion](#conclusion)

## 1.1 Introduction:
Decentralized finance (DeFi) has been one of the fastest-growing sectors in the blockchain industry. Educational DeFi (EduDeFi) is a subsector that provides a platform for users to contribute educational content and earn rewards. 
In this tutorial, I walk you through the process of building a simple Educational DEX Aggregator on Celo blockchain using Hardhat. taking to note how to create a smart contract that allows users to contribute educational content and earn rewards in the form of CELO tokens.

## 1.2 Learning Objectives
Objective:
~Ability to create a simple Educational DEX Aggregator on Celo blockchain using Hardhat.
~You will understand how to write and deploy smart contracts.
~Interact with them using a web3 interface, and how to use the Celo blockchain to store and transfer value.

## 1.3 Tech Stack:
stacks required to scale through the tutorial
* Hardhat
* Solidity
* JavaScript
* React
* Celo Blockchain
 
## 1.4 Prerequisites and Previous Knowledge:
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

## Setting up the Environment
### 2.1 Installing Node.js and NPM
### 2.2 Installing Hardhat

### 2.1 Installing Node.js and NPM
To get started, you need to have Node.js and NPM installed on your system. If you don't already have them installed, follow these steps to install them:

Go to https://nodejs.org/en/download/ and download the appropriate version for your operating system.
Run the installer and follow the prompts to install Node.js and NPM.
You can verify that Node.js and NPM have been installed correctly by running the following commands in your terminal:

run
		node -v
		npm -v


These commands should return the version number of Node.js and NPM respectively.

### 2.2 Installing Hardhat
Hardhat is a popular development environment for building Ethereum-compatible blockchain applications. It provides a suite of tools that make it easy to write, test, and deploy smart contracts.

To install Hardhat, run the following command in your terminal:

``` css
npm install --save-dev hardhat
```

This will install Hardhat as a development dependency in your project.

* 2.2 Creating the Project
* 2.3 Initializing the Project
* 2.4 Configuring Hardhat

## 2.3 Initializing the Project
To create a new project, create a new directory for your project and run the following commands in your terminal:

``` bash
mkdir edudefi-aggregator
cd edudefi-aggregator
npm init -y 
```

This will create a new directory for your project and initialize a new npm package in it.

## 2.4 Configuring Hardhat
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

* Creating the Smart Contract
* Defining the Smart Contract
* Compiling the Smart Contract

### 3.1 Defining the Smart Contract
Create a new file called EduDeFi.sol in the contracts directory and add the following code:
``` solidity
pragma solidity ^0.8.0;

contract EduDeFi {
    // Define data structures for educational content
    struct Content {
        address author;
        string title;
        string url;
    }

    // Define mapping to store educational content
    mapping(uint256 => Content) public contents;
    uint256 public contentCount;

    // Define event to emit when new content is added
    event ContentAdded(address indexed author, uint256 indexed id, string title, string url);

    // Define function to add new content
    function addContent(string memory _title, string memory _url) public {
        contents[contentCount] = Content(msg.sender, _title, _url);
        contentCount++;

        emit ContentAdded(msg.sender, contentCount - 1, _title, _url);
    }
}
```
* This contract defines a data structure for educational content
a mapping to store the content, and a function to add new content. The addContent function takes a title and a URL as input, creates a new Content struct with the sender's address, title, and URL, and adds it to the contents mapping. It also emits a ContentAdded event with the author's address, content ID, title, and URL.

### 3.2 Compiling the Smart Contract
To compile the smart contract, run the following command in your terminal:
``` python
npx hardhat compile
```

### This will compile the EduDeFi.sol contract and generate artifacts in the artifacts directory.

* Deploying the Smart Contract
* Setting up a Celo Network
* Configuring Hardhat for Deployment
* Deploying the Smart Contract

### 3.3 Setting up a Celo Network
Before deploying the smart contract, you need to set up a Celo network. Follow the instructions at https://docs.celo.org/getting-started/baklava-testnet to set up a Baklava testnet node.

### 3.4 Configuring Hardhat for Deployment
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

### 3.4 Deploying the Smart Contract
To deploy the smart contract, run the following command in your terminal:

```arduino
npx hardhat run scripts/deploy.js --network celo
```
This will deploy the EduDeFi contract to the Celo network and print the contract address to the console.

### 4.1 Interacting with the Smart Contract
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

### 4.4 Adding Content to the Smart Contract
To add content to the EduDeFi smart contract, follow these steps:

* Connect your Celo Wallet to the Celo network.
* Copy the contract address from the console after deploying the smart contract.
* In the Celo Wallet, click the "Contracts" tab and then "Add Contract".
* Paste the contract address into the "Contract Address" field and select the EduDeFi contract from the dropdown.
* Click "Add Contract" to add the contract to your Celo Wallet.
* In the "Write Contract" section of the contract, select the addContent function from the dropdown.
* Enter a title and URL for the content you want to add.
* Click "Write" to add the content to the smart contract.

### 4.5 Viewing Content on the Smart Contract
To view the content that has been added to the EduDeFi smart contract, follow these steps:

* Connect your Celo Wallet to the Celo network.
* Copy the contract address from the console after deploying the smart contract.
* In the Celo Wallet, click the "Contracts" tab and then "Add Contract".
* Paste the contract address into the "Contract Address" field and select the EduDeFi contract from the dropdown.
* Click "Add Contract" to add the contract to your Celo Wallet.
* In the "Read Contract" section of the contract, select the getContent function from the dropdown.
* Enter the ID of the content you want to view.
* Click "Read" to view the content.

### 5.0 Conclusion
In this tutorial, we have created a simple educational dex aggregator on the Celo blockchain using the Hardhat development framework. We have learned how to create a smart contract that stores educational content, how to deploy the smart contract to the Celo network, and how to interact with the smart contract using the Celo Wallet and Remix. We have also learned how to add content to the smart contract and view content stored on the smart contract. With this knowledge, you can start building your own educational dex aggregator and contribute to the Celo blockchain ecosystem.
