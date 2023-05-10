# Creating an Educational DAO on the Celo Blockchain with Solidity and Hardhat.md

 A tutorial based on how to create a dao on celo blockchain.
 
 ## INTRODUCTION
 A DEX aggregator is a platform that allows users to access multiple decentralized exchanges (DEXs) through a single interface, Instead of having to visit multiple DEXs to find the best price for a specific token, users can use a DEX aggregator to compare prices and execute trades on the DEX with the best available price.

DEX aggregators typically use smart routing algorithms to split orders into smaller parts and execute them across multiple DEXs. This can lead to better prices, lower slippage, and higher liquidity for users with fast transactions.

a popular DEX aggregator is the 1inch aggregator in the ethereum network. Matcha, and ParaSwap are as well popular platforms that offer a variety of features such as limit orders, price alerts, and portfolio tracking to make trading on DEXs more accessible and user-friendly.

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
*Hardhat
*Solidity
*JavaScript
*React
*Celo Blockchain
 
## 1.4 Prerequisites and Previous Knowledge:
To follow along with this tutorial, you should have basic knowledge of:

*Blockchain and its fundamental concepts
*Smart contract development using Solidity
*JavaScript and React
*Web3 interface and how to use it to interact with smart contracts

You will also need to install:
*Node.js
*NPM
*Hardhat
5.2.4 Time Required:
This tutorial is designed for beginners and can take up to 4 hours to complete.
However, the time required may vary depending on your proficiency with the tech stack and your familiarity with blockchain development, most importantly if you dont get attack by bugs, lol


Let's get started!

# Setting up the Environment
2.1 Installing Node.js and NPM
2.2 Installing Hardhat

2.1 Installing Node.js and NPM
To get started, you need to have Node.js and NPM installed on your system. If you don't already have them installed, follow these steps to install them:

Go to https://nodejs.org/en/download/ and download the appropriate version for your operating system.
Run the installer and follow the prompts to install Node.js and NPM.
You can verify that Node.js and NPM have been installed correctly by running the following commands in your terminal:

run
		node -v
		npm -v




