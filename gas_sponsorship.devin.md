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

4. Use Metaplex's `transferSol` instruction to send sols to the destination wallet, with `gas_sponsor` wallet
signing the transactiona and paying the gas fees: https://github.com/metaplex-foundation/umi/blob/main/docs/transactions.md#transaction-builders

5. Test the app, then push to the github repo passed by the user.
    - Show the deployed website to the user, then after confirming, generate PR ( only 1 PR ).

6. Send the latest URL of deployed website and the github repo with latest code to the user.
