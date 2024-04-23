Playbook: Create an ERC20 token.

## Procedure
1. **Set Up the Development Environment**:
   - Ensure you have Node.js and npm installed on your machine.
   - Install Hardhat by running `npm install --save-dev hardhat` in your project directory.
   - Initialize a new Hardhat project by running `npx hardhat init`.
   - Create a TS hardhat project.
   - Install OpenZeppelin contracts and Chai for testing by running `npm i @openzeppelin/contracts chai`.

2. **Create the ERC20 Token Contract**:
   - Ask the user for the name of the ERC20 token.
   - Copy the provided ERC20 token code into `MyToken.sol` ( MyToken is a placeholder, replace it with the token name ). This code includes the use of OpenZeppelin's ERC20, ERC20Capped, and ERC20Burnable contracts to create a token with a cap and burnable functionality.
   - Inside `MyToken.sol`, add the code to create a token with initial supply of 10000 tokens and token name = `Devil`, token symbol = `DEV`
   - This code includes the use of OpenZeppelin's ERC20, ERC20Capped, and ERC20Burnable contracts to create a token with a cap and burnable functionality.

3. **Configure Hardhat**:
   - Ask for the user's RPC endpoint.
   - Ask for user's private key to deploy the contract.
   - Save the above two in an Environment variable.
   - Intall 'dotenv' from npm.
   - Use dotenv to import the secrets from the Environment variable.
   - Edit the `hardhat.config.js` file to configure Hardhat for deployment after settig up the RPC endpoint for deployment to Sepolia testnet .

4. **Write Unit Tests** (Optional but recommended):
   - Use the `test` directory to write unit tests for your token. This helps in identifying and preventing potential issues.

5. **Deploy the Token Contract**:
   - Ensure you have enough ETH in your wallet for deployment. If deploying to a testnet like Sepolia, you can get test ETH from a faucet.
   - Modify the `scripts/deploy.js` file to include the deployment script for your token contract.
   - Deploy your contract by running `npx hardhat run --network sepolia scripts/deploy.js` in your terminal. 
6. **Interact with the Token**:
   - Test the token address on Etherscan Sepolia to verify that the deployment was successful.
   - Returnt the Etherscan sepolia explorer link of the deployed token. 
