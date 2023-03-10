# AAVE Flash Loan Template

This is a template for creating a flash loan on the AAVE protocol.

> **Note** **Check the [`arbitrage`](https://github.com/princeibs/flashloan-template/tree/arbitrage) branch for an example of implementing arbitrage with flash loans.**

All AAVE's core contracts and interfaces are already included in the template. Locate the `Flash` contract in the Flash.sol file to add your logic. 

### How to test (Using [Remix IDE](https://remix.ethereum.org))
1. Request for some DAI from [AAVE faucet](https://app.aave.com/faucet/).

2. Add the DAI token address to your wallet. (Note that this is AAVE's version of DAI and might be different from the one you have already).
`0xDF1742fE5b0bFc12331D8EAec6b478DfDbD31464` is **AAVE's DAI token address** for now. This might be subject to change in the future.

3. Deploy `Flash` contract inside `contracts/Flash.sol` file on the Remix IDE interface using the "Pool Address Provider - AAVE" address found [here](https://docs.aave.com/developers/deployed-contracts/v3-testnet-addresses). 
<img width="354" alt="image" src="https://user-images.githubusercontent.com/64266194/212767909-5c718e2e-8e03-41ba-8265-cdc5e89db561.png">

4. Send 1 DAI to the deployed contract. A very small amount will be deducted and used to pay back interest when returning loaned amount to AAVE.

5. From the Remix IDE interface, click on the `requestFlashloan` button and pass in AAVE's DAI token address as the first parameter and the amount you want to borrow as the second parameter. Append 18 zeros to the amount to handle DAI's decimal.
<img width="354" alt="image" src="https://user-images.githubusercontent.com/64266194/212767548-b6156ed3-bf36-424a-b0cb-2552727c5137.png">

6. When the transaction is complete, view it on etherscan and you will find something similar to this
![image](https://user-images.githubusercontent.com/64266194/212847347-04fde781-ca69-4689-a8a2-2347a2609232.png)
From the image above:
 * AAVE's contract sent 100 DAI to my contract.
 * My contract obviously did nothing with it because I didn't add any logic.
 * My contract returned the borrowed DAI (plus interest) back to AAVE. **_.05_** DAI attached to the amount my contract is sending back is the interest I paid for the loan. So before calling the `requestFlashloan` method, ensure there is enough funds in your contract to pay for the interest.
 
 **Check the [`arbitrage`](https://github.com/princeibs/flashloan-template/tree/arbitrage) branch of this repo to see a mini example on how flash loans can be used to perform arbitrage on two DEXes with token price differences**

