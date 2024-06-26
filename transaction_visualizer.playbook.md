Playbook: Data visualization of a wallet's transaction on Ethereum

## Overview

The task is to create a simple web app using React, which can connect to MetaMask wallet and fetch all the transaction data for the connected wallet and create a data visualization from it.

## Procedure

1. Create a React app ( using `create-react-app` )
2. Install `Ethers.js`, `axios`, `react-paginate`
3. Build a beautiful UI and create a Button to Connect to MetaMask
   - Use the color scheme of Netflix or Hotstar and create properly visible components.
   - In App.js, create a button that will trigger the MetaMask connection when clicked.
   - set up a state to hold the connected account's address.
   - Mock connection to MetaMask for testing if the app can connect to metamask and test if the app is working.
4. Fetch Transactions Using Etherscan API
   - Ask the user for the Etherscan API key ( store it safely )
   - Using the etherscan sepolia api, fetch all the transactions on `Sepolia Testnet` from the wallet address using axios ( `GET` request )
5. Create a Data Visualization with Pagination
   - For data visualization, use `React Table` library
   - For pagination, you use `react-paginate` library
   - The table must contain 4 columns : transactionAddress, from, to, timeStamp
   - One page should contain only 8 transactions
6. Deployment and Push to GitHub:
   - Before deployment, remove all the mock data and mocking logic, so that the app shows real transactions for the connected wallets.
   - After deploying the application and testing it, prepare for pushing the code to GitHub
   - ask the user for an `https` link for the repo to push the code to
   - while making any changes to the code, create a separate branch for the changes and generate PR, and make sure if the topic for change is same, don't create a separate `pr` for it
   - follow the best branch naming practices for the github branches

## Specification

- Project name should be `transaction-explorer`

## Forbidden Actions

- Don't try to login to metamask as you can't use the metamask extension.
- Don't waste time on fixing `npm install` warnings and vulnerabilities, if they don't break the app.
- Don't `push` the code to a repo before confirming from the user.
- Don't use the mock data while deployment.

## Advice and Pointers

- The API endpoint of Etherscan sepolia is this: https://api-sepolia.etherscan.io/api

- If the etherscan api doesn't work properly, use this API endpoint: - Etherscan API: `https://api.etherscan.io/api?module=account&action=txlist&address=${account}&startblock=0&endblock=99999999&sort=asc&apikey=${apiKey}`

- If even this endpoint doesn't work properly, use this another endpoint: `http://api.etherscan.io/api?module=account&action=txlist&address={account}&sort=asc`

- Before deployment, make sure the `Connect Wallet` button is working properly, and remove the mocking code and mock data before deployment.
