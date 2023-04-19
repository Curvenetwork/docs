# Token Bridges

We have two bridges as explained below

1. Curve Bridge:  ****The bridge, based on POA's bridge implementation, is used to transfer Curve tokens between the Curve chain and the Ethereum network.
2. TL20 token bridge: This bridge is used to transfer TL20 tokens into Curve chain and back. Please not that Curve bridge is not supposed to be used to transfer  . 

The bridge, based on POA's bridge implementation, is used to transfer Curve tokens between the Curve chain and the Ethereum network.

Tokens sent to the respective bridge contract on one network \(whether it's Curve or Ethereum\) are "locked" in the bridge, "unlocked" on the other network bridge and transferred to the sender.

The validators of the bridge on both network are the Curve chain validators. This means that validators, as part of their governance responsibilities, also need to validate bridge transactions and therefore hold Curve tokens to "approve" bridge transactions on Curve chain and hold ETH to "approve" transactions on Ethereum.

Each bridge transaction must be approved by a majority \(over 50%\) of the validators in order to be processed successfully.

The bridge contracts are deployed on both networks, and bridge oracle processes run on each validators machine as part of the validator deployment stack.

Besides the transfer of Curve tokens between the two networks, the bridge is also responsible for network core functionality events:

**Mint block reward distributed on the Curve chain on Ethereum**

Each cycle the total block reward distributed on Curve chain is minted on Ethereum and locked on the bridge contract.

This works by listening to the \`RewardedOnCycle\` event emitted by the BlockReward contract on Curve chain, waiting for all bridge validators on Curve chain to sign it, and eventually sending a transaction to mint on Ethereum \(by the last signing validator\).

**Update Curve chain validators on Ethereum**

Each cycle the Curve chain validators are selected from a random snapshot of pending validators.

Those validators, being also the bridge validators, need to be updated on Ethereum as well.

This works by listening to the \`InitiateChange\` event emitted by the Consensus contract on Curve chain, waiting for all bridge validators on Curve chain to sign it, and eventually sending a transaction to set the bridge validators on Ethereum \(by the last signing validator\).

{% hint style="info" %}
Curve chain bridge - [0xd617774b9708F79187Dc7F03D3Bdce0a623F6988](https://curvescan.io/address/0xd617774b9708f79187dc7f03d3bdce0a623f6988)

Ethereum bridge - [0xC50Ca7Ead738F5501F5EF88F6015d7F09D238F95](https://etherscan.io/address/0xC50Ca7Ead738F5501F5EF88F6015d7F09D238F95)

Curve token on Ethereum - [0x970B9bB2C0444F5E81e9d0eFb84C8ccdcdcAf84d](https://etherscan.io/token/0x970B9bB2C0444F5E81e9d0eFb84C8ccdcdcAf84d)
{% endhint %}

**Using the bridge**

**Transfering from Ethereum mainnet to Fusenet** - Send your erc20 Curve tokens to the Ethereum bridge for them to be released from the Curve chain bridge and be avaliable in your native Curve wallet.

**Transfering from Fusenet to Ethereum mainnet** - Send your Native Curve tokens to the Curve chain bridge for them to be released from the mainnet bridge and be avaliable in your Mainnet wallet. 

