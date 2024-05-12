## Overview

The Playbook guides you through how to create a simple zero knowledge proof and verify it on the Ethereum blockchain.

## What's Needed From User

- `SEPOLIA_PRIVATE_KEY`
- `INFURA_API_KEY`

## Specification

- Use `Sepolia Eth` testnet for deploying the smart contract.
- Use the circom docs for getting sample `Multiplier` circuits: https://docs.circom.io/getting-started/writing-circuits/
- The circuit name should be `Multiplier`

## Procedure

1.  Circom and dependencies setup

    - install rust: `curl --proto '=https' --tlsv1.2 [https://sh.rustup.rs](https://sh.rustup.rs/) -sSf | sh`
    - build circom from source:
      `git clone [https://github.com/iden3/circom.git](https://github.com/   iden3/circom.git)`
      `cd circom`
      `cargo build --release`
      `cargo install --path circom`
    - install snarkjs: `npm install -g snarkjs`
    - create a working directory: `mkdir zk_tuts && cd zk_tuts`

2.  Create and compile the circuit

    - create a basic circuit (add a `multiplier.circom` file to the root directory), which using inputs `a` and `b`, generates a product `c`, which is equal to `a*b`.
    - compile the circuit: `circom multiplier.circom --r1cs --wasm --sym --c`
    - verify that a `multiplier.r1cs` file and a `multiplier.wasm` file is generated after compilation of the circuit
    - print info on the circuit: `snarkjs r1cs info multiplier.r1cs`

3.  Generate the witness

    - create an `in.json` file at the root, and inside it, define the inputs `"a":5, "b":6`
    - print the contents of the `in.json` file
    - generate witness by running command: `node multiplier_js/generate_witness.js multiplier_js/multiplier.wasm in.json witness.wtns` at the root of the project
    - display the witness: `snarkjs wtns export json witness.wtns witness.json`
    - print the `witness.json` file contents

4.  Generate the proof

    - download the `powers of tau` file: `wget https://hermez.s3-eu-west-1.amazonaws.com/powersOfTau28_hez_final_11.ptau`
    - generate the verification key: `snarkjs plonk setup multiplier.r1cs powersOfTau28_hez_final_11.ptau multiplier.zkey`
    - get a verification key in json format (from the proving key): `snarkjs zkey export verificationkey multiplier.zkey verification_key.json`
    - generate the proof: `snarkjs plonk prove multiplier.zkey witness.wtns proof.json public.json`
    - verify that the above command generates a `proof.json` file and a `public.json` file.
    - verify the proof by running : `snarkjs plonk verify verification_key.json public.json proof.json`

5.  Verify the proof via a smart contract

    - generate a solidity verifier smart contract: `snarkjs zkey export solidityverifier multiplier.zkey verifier.sol`
    - verify that the above command genrates a file named `verifier.sol`
    - generate solidty calldata: `snarkjs zkey export soliditycalldata public.json proof.json`
    - copy the result of the above command into a file named `calldata.txt`

6.  Creat a simple hardhat project

    - create a `hardhat` folder and `cd` into it
    - install hardhat:
      `npm init`
      `npm install --save-dev hardhat`
      `npx hardhat init`
      Select Create an empty `hardhat.config.js`
    - Install `hardhat toolbox`: `npm install --save-dev @nomicfoundation/hardhat-toolbox`
    - Append `require("@nomicfoundation/hardhat-toolbox");` to the top of `hardhat.config.js`
    - Ask the user for `SEPOLIA_PRIVATE_KEY` and `INFURA_API_KEY` and store them in `.env` file
    - Configure `hardhat.config.js` to use `Sepolia ETH` testnet for deployment:

    ```require("@nomicfoundation/hardhat-toolbox");

     const { vars } = require("hardhat/config");

     const INFURA_API_KEY = vars.get("INFURA_API_KEY");

     // Add your Sepolia account private key to the configuration variables
     const SEPOLIA_PRIVATE_KEY = vars.get("SEPOLIA_PRIVATE_KEY");

     module.exports = {
     solidity: "0.8.24",
     networks: {
         sepolia: {
         url: `https://sepolia.infura.io/v3/${INFURA_API_KEY}`,
         accounts: [SEPOLIA_PRIVATE_KEY],
         },
     },
     };
    ```

    - put the Verifier.sol contract in the `contracts` folder.

7.  Compile and deploy the contract - compile the contract `npx hardhat compile` - create deployment script:
    `mkdir scripts && echo > scripts/deploy.js` - put this code inside `deploy.js`:

        ````async function main() {

            const [deployer] = await ethers.getSigners();

            console.log(
            "Deploying contracts with the account:",
            deployer.address
            );

            const Verifier = await ethers.getContractFactory("Verifier");
            const contract = await Verifier.deploy();

            console.log("Contract deployed at:", contract.address);

            const proof_verification = await contract.verifyProof(calldata);

            console.log("Proof verification status:", proof_verification);

        }

        main()
        .then(() => process.exit(0))
        .catch(error => {
        console.error(error);
        process.exit(1);
        });
        ````

    - pass the content of `calldata.txt` file to the `verifyProof()` function call in the `deploy.js` script.
    - deploy the contract: `npx hardhat run scripts/deploy.js --network sepolia`

## Advice and Tips

- Keep `SEPOLIA_PRIVATE_KEY` and `INFURA_API_KEY` in `.env` file and handle them carefully.
- Push the code to a new repo named `zk-proof-sample` in the `Devin-Applications` organisation.
- Use the commands excatly as they are provided in the procedure.
