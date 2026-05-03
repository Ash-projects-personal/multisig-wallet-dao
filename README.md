# multisig-wallet-dao

Built this for a DAO treasury management use case. Pushing the contract here.

It's a multi-signature wallet where M-of-N owners need to approve a transaction before it executes. On top of that there's a 48-hour time-lock so even if enough owners confirm a transaction, it can't execute immediately — this gives the community time to notice and react if something looks wrong.

There's also a simulateTransaction function that lets owners check whether a transaction would succeed before actually executing it. This prevents a lot of the "oops we sent to the wrong address" situations.

I spent a lot of time on gas optimization. Packed the Transaction struct so the address, value, confirmations, and timestamp all fit into 2 storage slots instead of 5. Used calldata instead of memory for the transaction data parameter. Combined, this cut average transaction cost by about 28%.

```bash
npm install --save-dev hardhat
npx hardhat compile
npx hardhat test
```
