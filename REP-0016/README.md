# REP-0016: Hard fork Ronin chain to upgrade the Axie and Land smart contracts

## Preamble

<pre>
REP-0016
Title: Hard fork Ronin chain to upgrade the Axie and Land smart contracts
Author: Owl Of Moistness (discord: owlofmoistness)
Type: Network/standard
Status: Draft
Created: 2024-05-12
</pre>


## Abstract

REP-0016 describes the process of hardforking the current Ronin blockchain to replace the bytecode residing in the Axie and Land smart contracts with an ERC-1967 Transparent Proxy standard that will enable us to update the implementation in the future without any hardforks. On top of that, those contracts will inherit from REP-0015 standard for Ownership Delegation.


## Rationale

Due to the current nature of the existing Axie and Land smart contracts, it is impossible to upgrade the contracts freely to add new features without performing a migration or new minting of assets. Such operations are extremely heavy and a waste of space given the amount of assets to manage during this operation. A simpler solution is to hardfork the chain and override the bytecode in the contracts to go directly to an ERC-1967 transparent proxy. Down the line, we shall be able to upgrade contracts by simply updating the implementation which is a much easier approach than migrations or hardforks.


## Specification

The Axie and Land smart contract shall be paused to ensure no transfers occur during the hardfork/upgrade. Additionally, this pausing feature should be present in the new proposed implementations.

A specific block will be agreed upon in the short term future from which onwards the fork will happen. Validators will need to have updated their software to make sure they support the hardfork and ensure smooth online service. 

The bytecode of the Axie and Land smart contract will need to be updated to the standard ERC1967 bytecode. On top of that the storage slot of the owner of the proxy shall have to be set to a multisig controlled by relevant parties (validators, axie committee, sky mavis reps etc).

Upgrade of the implementation shall be voted on in the future before being pushed on chain.


## Reference

REP-0015: <https://github.com/ronin-chain/REPs/blob/main/REP-0015/REP-0015.md> 

ERC-1967 : <https://eips.ethereum.org/EIPS/eip-1967>


## Security analysis

The main risk is to set up the wrong storage point offset in the new contract implementation. This could result in data loss and corruption. 
Another risk is ensuring correct ownership of the proxy and asset contract to make sure no malicious actor can executed functions to create DoS or seek advantages.


## License

The content is licensed under [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
