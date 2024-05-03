Playbook: Create a fungible token in Solana using Metaplex

## Overview

Create a Next JS app which can create, mint and transfer fungible tokens to any wallet on Solana

## Procedure

1. Instantiate the project: ( App name is TokenX )

   - Install `Next JS`, `@metaplex-foundation/mpl-token-metadata`, `@metaplex-foundation/mpl-toolbox`, `@metaplex-foundation/umi`, `@metaplex-foundation/umi-bundle-defaults`, `@metaplex-foundation/umi-uploader-irys`, `@solana/spl-token`, `@solana/wallet-adapter-react`, `react-toastify`
   - Install and setup `Acertinity UI`( docs: https://ui.aceternity.com/ )

2. Design the frontend of the web app:

   - Create a landing page using Acertinity UI, with a Try Now button
   - The button redirects to the page with navbar header `TokenX`, and containing a mutli-choice form, with options:
     `Create Token`, `Mint Token`, `Send Token`
   - The navbar also contains the `Connect Wallet` button from solana wallet adapter Multiwallet button.
   - On connecting wallet, display all the tokens that the wallet holds ( use `fetchAllDigitalAssetByOwner`, `getAssociatedTokenAddress`, `getTokenAccountBalance`) and display `token name`, `symbol` and `balance` in a tabular form.

3. Implementing token creation, minting and transfer operations:

   - The user can either create a new token ( using `createFungible` instruction from Metaplex), or
   - Go to the mint tokens form, use `mintV1` instruction from Metaplex to mint already created tokens.
   - User can select from a dropdown, the tokens they can mint, and then pass the number of tokens to mint of that particular token
   - Mint button to trigger the mintV1 instruction.
   - A form similar to Mint token for Transfer Token, with fields select token, transfer amount, destination wallet.
   - Use `transferTokens` instruction to send token.

4. Test and deploy the project.

   - Be sure to remove the mock data and mocking functions, and use the real data only

5. Push the code to github:
   - Ask the HTTPS repo URL
   - Create a unique PR ( don't create separate PR for same functionality/ bugfix)

## Forbidden Actions

- Don't try to login to Phantom or any other EOA wallet as you can't use the metamask extension.
- Don't waste time on fixing `npm install` warnings and vulnerabilities, if they don't break the app.
- Don't `push` the code to a repo before confirming from the user.
- Don't use the mock data while deployment.

## Advice and Pointers

- Helius RPC endpoint: https://devnet.helius-rpc.com/?api-key=7514a7bd-79b3-44f0-b42b-8db3c48038a7

- read this repo for reference: https://github.com/FuryACE007/minter-tauri.git, and focus on `useUmi.ts` and `WalletComponent.tsx`

- `WalletComponet.tsx` would contain all the functions we need to implement, use them for reference`
