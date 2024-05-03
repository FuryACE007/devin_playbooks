Playbook: Create a Solana dApp for transferring SOLs to another account

## Overview

The task is to create a dApp on Solana for transferring SOLs to another account, but the transaction fees for sending sols would
be covered by a fixed `gas_sponsor` wallet.

## Procedure

1. Project setup using Next JS ( use `pnpm` )

   - Use Material UI as the styling library
   - Install Metaplex umi: https://github.com/metaplex-foundation/umi
   - Setup Umi properly ( for End Users ) as per the docs.
   - Ask the user for the devnet RPC endpoint with API_KEY.
   - Install Solana wallet adapter and set it up: https://docs.magiceden.io/docs/using-the-solana-wallet-adapter

2. Create the ui for token transferring

   - Use MUI to create form for sending data to another wallet.
   - Add wallet button

3. Setup the `gas_sponsor` wallet, and add it as the signer for the umi instance.

   - Ask for the sponsor wallet private key
   - Save it securely
   - Generate signer using the Private, and set it as the signer in Umi instance.

4. Use Metaplex's `transferSol` instruction to send sols to the destination wallet, with `gas_sponsor` wallet

- signing the transactiona and paying the gas fees: https://github.com/metaplex-foundation/umi/blob/main/docs/transactions.md#transaction-builders

5. Test the app, then push to the github repo passed by the user.
   - Show the deployed website to the user, then after confirming, generate PR ( only 1 PR ).

## Specification

- Github url: https://github.com/FuryACE007/send_sol
- The Next JS project should be created with an app directory and without app router.

## Advice and Pointers

- Use `@metaplex-foundation/umi` instead of directly using `@solana/web3js`
- https://github.com/FuryACE007/minter-solana/blob/main/src/useUmi.ts -> This is how you setup umi hook
- https://github.com/FuryACE007/minter-solana/blob/835490d88cf0d3b2f0a89f50b8f2d0e802a54b6c/src/WalletComponent.tsx#L67 -> This is how you instantiate a `Umi` instance
- This is how you generate signer from private key:

````const { Keypair } = require('@solana/web3.js');

// Replace with your private key string
const privateKeyString = 'your_private_key_string';

// Convert the private key string to a Uint8Array
const privateKeyBytes = Uint8Array.from(privateKeyString.split(','));

// Generate a Keypair from the private key bytes
const signer = Keypair.fromSeed(privateKeyBytes);```
````
