# Building a Common Good Parachain Oracle Using Phala as a Feed

## Motivation
The lack of an oracle primitive in the Dotsama ecosystem has been addressed with the original proposal for a federated and decentralized parachain oracle system [here](https://forum.polkadot.network/t/help-us-create-a-federated-and-decentralised-parachain-oracle-system/1190). Further discussion can be found [here](https://forum.polkadot.network/t/oracles-for-polkadot/1286). This has prompted the development of a MVP towards creating a common good parachain, leveraging Phala's secure and private oracle system. This feature and the associated framework will be submitted with a grant application to the Web3 Foundation.

## Targets
+ MVP for a Common Good Parachain Oracle 
  + Ink contract around a Phat contract
  + Reporter registration and feed management
  + Create query 
  + Consume feed
  + Reporter inputs/aggregation  
  + Direct Integration
  + Business logic
  + Reporter staking/reward/slash
  + Fees
  + Fund Feed
  + Reporter Phat contract
  + Factory Phat contract

## Investigation and Design
This proposal will be implemented by a native smart contract using Ink! around Phat contracts.

## Milestones
+ **[~2022.12.26]** Installation (3K)
  + Reporter registration
  + XCM to fund data feeds 
  + Feed management (route orders according to matching between demand and supply of feeds)
+ **[~2023.01.17]** Business logic & Phala integration (12K)
    + Reporter staking/reward/slash
    + Fees
    + XCM create query
    + Phat keepers
+ **[~2023.02.13]** Second payment (15K)
  + Reporter inputs/aggregation  
  + XCM consume feed
  + Direct Integration
+ **[~2023.02.13]** Third payment (15K)

## Conclusion
Phala's secure and private feeds are ideal for creating a common good parachain oracle. This proposal will provide a secure and reliable data feed for the Dotsama ecosystem.